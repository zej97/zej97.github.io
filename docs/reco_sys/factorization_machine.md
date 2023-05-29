---
layout: default
title: Factorization Machine
parent: Recommendation System
nav_order: 1
---
# Factorization Machine is All You Need (maybe)
## Backgorund
The polynomial model is widely regarded as one of the most intuitive models for incorporating feature combinations. It allows for the explicit modeling of interactions between features by including polynomial terms in the model. By considering feature combinations of different degrees, the polynomial model captures non-linear relationships and can provide a more expressive representation of the data. 

The combination of features $x_i$ and $x_j$ is represented by $x_ix_j$, and the combination feature is only meaningful when both are nonzero. From a comparative perspective, this article only discusses the second-order polynomial model. The expression of the model obtained by adding second-order feature combinations to the traditional linear model is as follows:

$$
y({\rm \bf x}) = w_0 + \sum_{i = 1}^nw_ix_i + \sum_{i = 1}^n\sum_{j=i+1}^nw_{ij}x_ix_j \tag{1}
$$

The training and updating of parameters $w_{i, j}$ requires numerous non-zero $x_i$ and $x_j$ samples. However, due to the sparsity of the data (one-hot encoding for category features), most features are zero. 
For example, the following three features (Country, Day, Ad_type) are all categorical, and they need to be one-hot encoded into numerical value.

| Clicked | Country=USA | Country=FRA | Country=CN | Day=4/2/23 | Day=7/3/23 | Day=5/4/23 | Ad_type=Food | Ad_type=Car | Ad_type=Book |
|:-------:|:-----------:|:-----------:|:--------:|:----------:|:----------:|:--------:|:------------:|:-----------:|:--------:|
|    1    |      1      |      0      |    0     |      0     |      1     |    0     |       1      |      0      |    0     |
|    0    |      0      |      1      |    0     |      1     |      0     |    0     |       0      |      1      |    0     |
|    0    |      0      |      0      |    1     |      0     |      0     |    1     |       0      |      0      |    1     |

In this case, ${\rm \bf x} = (x_0, x_1, x_2, \cdots, x_7, x_8)$, where $x_{0, 1, 2}$ represents the one-hot encoding of the `country` feature, $x_{3, 4, 5}$ represents the one-hot encoding of the `day` feature, and $x_{6, 7, 8}$ represents the one-hot encoding of the `ad_type` feature.  As we can see, the number of nonzero elements in ${\rm \bf x}$ is very small, and the number of nonzero elements in $x_ix_j$ is even smaller. That leads to insufficient training for the model and poor generalization ability. Therefore, we need to introduce factorization machines (FM, 2010)[^1] to solve this problem.

It's true that compared to more advanced machine learning algorithms such as deep neural networks (DNNs), graph neural networks (GNNs), or attention-based models, Factorization Machines (FM) may appear relatively outdated. However, FM continues to be extensively used in the industry due to its fundamental role in recommendation systems. If you find yourself working at a startup and facing the task of building a recommendation system from the ground up, FM proves to be an excellent option.

**FM has the following advantages**:
1. Efficiency. FM is easy to develop, and fast to train, deploy, and maintain.
2. Interpretability. It is easy to understand the model and the feature importance. Moreover, the interpretability of FM helps us position the problems (bugs) quickly.
3. Preformance. We can't say that FM's performance is better than other models. However, it is a good baseline model for recommendation systems.

## Mechanism
The main idea of FM is to decompose the second-order feature combinations into the product of first-order feature combinations. That is, decoposing the elements of the cooccurrence matrix into the product of the user's latent vectors and the item's latent vectors - $\langle \mathbf{v}_i, \mathbf{v}_j \rangle$. Then we have the mathematical expression of FM as follows:

$$
\hat y(\mathbf{x}\vert\Theta) = w_0+ \sum_{i=1}^n w_i x_i + \sum_{i=1}^n \sum_{j=i+1}^n \langle \mathbf{v}_i, \mathbf{v}_j \rangle x_i x_j \tag{2}
$$
    
where $\Theta = (w_0, \mathbf{w}, \mathbf{V})$ is the model parameters. The latent factor matrix $\mathbf{V}$ is a $n \times k$ matrix, where $n$ is the number of features, and $k$ is the dimension of the latent factor. $\mathbf{v}_i, \mathbf{v}_j\in \mathbb{R}^k$ represnt the latent factor of feature $x_i$ and $x_j$ separately. Therefore, the inner product $\langle \mathbf{v}_i, \mathbf{v}_j \rangle$ is the feature interaction between $x_i$ and $x_j$:

$$
\langle \mathbf{v}_i, \mathbf{v}_j \rangle = \sum_{f=1}^k v_{i,f}v_{j,f} \tag{3}
$$

Does this look familiar? Yes, that is what embedding is. The nature of FM is to embed features. The latent factor $\mathbf{v}_i$ is the embedding of feature $x_i$. The inner product $\langle \mathbf{v}_i, \mathbf{v}_j \rangle$ is the similarity between the embeddings of $x_i$ and $x_j$. Note that $\mathbf{v}_i$ and $\mathbf{v}_j$ are in the same matrix $\mathbf{V}$, even if they are different type of feautres (e.g. users or items).

But why does embedding help when there are numerous sparse features? And why people say that FM has strong generalization ability? The answer is that if two features $x_i, x_j$ have never appeared together in the training set, the embedding $\mathbf{v}_i$ ($\mathbf{v}_j$) corresponding to $x_i$ ($x_j$) are still learned if $x_i$ appears with other features. Therefore, the inner product $\langle \mathbf{v}_i, \mathbf{v}_j \rangle$ can still be calculated when inferencing even if $x_i$ and $x_j$ have never appeared together in the training set.

## Formulation Optimization
### Optimze the second-order feature interaction
The time complexity of equation $(2)$ is $O(kn^2)$. With following optimization, we can reduce the time complexity to $O(kn)$.

$$
\begin{align*}&\sum_{i=1}^n \sum_{j=i+1}^n \langle \mathbf{v}_i, \mathbf{v}_j \rangle x_i x_j \\ &= \frac{1}{2}\sum_{i=1}^n\sum_{j=1}^n \langle \mathbf{v}_i, \mathbf{v}_j \rangle x_i x_j - \frac{1}{2}\sum_{i=1}^n \langle \mathbf{v}_i, \mathbf{v}_i \rangle x_i x_i\end{align*} \tag{4}
$$

The RHS of equation $(4)$ derives from the $\langle \mathbf{V}, \mathbf{V} \rangle$ subtracting the redundant diagonal elements $\langle \mathbf{v}_i, \mathbf{v}_i \rangle x_i x_i$. 

Then we unfold the summation according to $(3)$ and get the following equation:

$$
(4) = \frac{1}{2}\sum_{f = 1}^k \left(\left(\sum_{i = 1}^n v_{i,f} x_i\right)^2 - \sum_{i = 1}^n v_{i, f}^2 x_i^2\right) \tag{5}
$$

Eventually, the time complexity of equation $(5)$ is $O(kn)$.

### Optimzation in the Recall Stage
In the recall stage, we need to calculate the similarity between the embedding of the user and the embedding of the item. The time complexity of equation $(5)$ is $O(kn)$, where $n$ is the number of features. If we have a large number of features, the time complexity will be very high. Therefore, we need to optimize the recall stage.

We decompose the second-order feature interaction into the sum of the term of users and the term of items. Then we get the following equation:

$$
\begin{align*}&(5) = \frac{1}{2} \sum_{f=1}^{k}\left(\left(\sum_{u \in U} v_{u, f} x_{u} + \sum_{t \in I} v_{t, f} x_{t}\right)^{2}-\sum_{u \in U} v_{u, f}^{2} x_{u}^{2} - \sum_{t\in I} v_{t, f}^{2} x_{t}^{2}\right) \\ &= \frac{1}{2} \sum_{f=1}^{k}\left(\left(\sum_{u \in U} v_{u, f} x_{u}\right)^{2} + \left(\sum_{t \in I} v_{t, f} x_{t}\right)^{2} \\ + 2{\sum_{u \in U} v_{u, f} x_{u}}{\sum_{t \in I} v_{t, f} x_{t}} - \sum_{u \in U} v_{u, f}^{2} x_{u}^{2} - \sum_{t \in I} v_{t, f}^{2} x_{t}^{2}\right) \end{align*}\tag{6}
$$

Where the $U$ and $I$ are the set of users and items respectively. The $x_u$ and $x_t$ are the user's feature vector and the item's feature vector respectively. 

For the same user, even when they interact with different items, the scores of the first-order and second-order interaction terms between user features remain constant. This implies that it does not impact the final sorting result. Therefore, the formula can be simplified again by **removing the user internal interaction features**, and get the matching score of the user and the item:

$$
\begin{align*}&\text{MatchScore}_{FM} = \mathbf{W}_t + \mathbf{V}_{tt} + \mathbf{V}_{ut} \\ &=\sum_{t \in I} w_{t} x_{t} + \frac{1}{2} \sum_{f=1}^{k}\left(\left(\sum_{t \in I} v_{t, f} x_{t}\right)^{2} - \sum_{t \in I} v_{t, f}^{2} x_{t}^{2}\right) + \sum_{f=1}^{k}\left( {\sum_{u \in U} v_{u, f} x_{u}}{\sum_{t \in I} v_{t, f} x_{t}} \right) \end{align*}\tag{7}
$$

## Parameter Update

### Parameter Gradient Update[^2]

FM parameters:

$$
\Theta= \lbrace w_0, \mathbf{w}, \mathbf{V}\rbrace = \lbrace w_0,w_1,…,w_n,v_{1,1},…,v_{n,k}\rbrace \tag{8}
$$

where $w_0$ is the bias term, $\mathbf{w}$ is the first-order feature weight vector, and $\mathbf{V}$ is the second-order feature interaction matrix.

If we regard the $\hat{y}(x\vert\Theta)$ as a binary classification problem, we can use the logistic loss function to optimize the parameters. For binary classification task, we need a sigmoid function to transform the output of the model to the probability of the positive class:

$$
P(y = 1 \vert x, \Theta) = \frac{1}{1 + \exp(-\hat{y}(x|\Theta))} = \sigma(\hat{y}(x|\Theta)) \tag{9}
$$

If we assign 1 to the positive class (clicked) and -1 to the negative class (not clicked), the probability of the positive class can be expressed as:

$$
P(y\vert x, \Theta) = \frac{1}{1 + e(-y\hat{y}(x|\Theta))} = \sigma(y\hat{y}(x|\Theta)) \tag{10}
$$

The parameters estimation can be calculated by the maximum likelihood estimation method. For training data set $S$, the optimal problem would be:

$$
\argmax_{\Theta}\prod_{(x, y) \in S} P(y|x, \Theta) = \argmin_{\Theta} \sum_{(x, y) \in S} -\ln P(y|x, \Theta) \tag{11}
$$

Therefore, the loss function for one sample $(x, y)$ is:

$$
\ell(y\vert x, \Theta) = - \ln P(y|x, \Theta) = - \ln \sigma(y\hat{y}(x|\Theta)) \tag{12}
$$

Calculate the derivation of the loss function with respect to the parameter $\hat{y}$:

$$
\frac{\partial \ell}{\partial\hat{y}}=y(\sigma(y\hat{y})-1) \tag{13}
$$

Then, calculate the derivation of the $\hat{y}$ with respect to the parameter $\theta$:

$$
\frac{\partial\hat{y}}{\partial\theta}= \begin{cases} 1, & \text{if }\theta\text{ is }w_0, \\ x_i, & \text{if }\theta \text{ is }w_i, \\ x_i\sum_{j=1}^nv_{j,f}x_j-v_{i,f}x_i^2 & \text{if }\theta\text{ is }v_{i,f}. \\ \end{cases} \tag{14}
$$

Finally, we can get the derivation of the loss function with respect to the parameter $\theta$:

$$
g_0^w=\frac{\partial l}{\partial w_0}=y(\sigma(y\hat{y})-1)\\ g_i^w=\frac{\partial l}{\partial w_i}=y(\sigma(y\hat{y})-1)x_i\\ g_{i,f}^v=\frac{\partial l}{\partial v_{i,f}}=y(\sigma(y\hat{y})-1)(x_i\sum_{j=1}^nv_{j,f}x_j-v_{i,f}x_i^2) \tag{15}
$$

In the industry, the most commonly used optimization algorithm is the **stochastic gradient descent (SGD)**. SGD supports online learning naturally. If we use only one sample to update the parameters, SGD becomes the **online gradient descent (OGD)**. 

$$
\mathbf{w}_{t+1} = \mathbf{w}_t - \eta_t \nabla \ell(\mathbf{w}_t) = \mathbf{w}_t - \eta_t \mathbf{g}_t \tag{16}
$$

While OGD may perform well in the online learning scenario, it is not efficient enough as it cannot sparsify the parameters. The reason is that $\mathbf{g}_t$ is calculated by only one sample at a time, which can be highly random. Even with L1 regularization, it can be still difficult to find a sparse solution. Therefore, Google introduced the **Follow-the-Regularized-Leader** (FTRL)[^3] algorithm as a solution for parameter optimization. FTRL not only ensures superior performance of the model but also possesses the ability to sparsify parameters in online learning scenarios.

## Insights
When traning the model, if we only have the user features and item features, the size $n$ of the one-hot vector $x$ is the sum of the number of users and the number of items. The size of the second-order feature interaction matrix $\mathbf{V}$ is $n \times k$. This latent matrix $V$ is also the ***table*** where stores the user and item embeddings. The size of each embedding is $k$.

Furthermore, it is obvious the following two terms are the equivalent:

$$
\sum_{u\in U}\sum_{t\in I}\langle \mathbf{V}^{\rm T}x_u, \mathbf{V}^{\rm T}x_t\rangle \tag{17}
$$

$$
\langle \sum_{u\in U} \mathbf{V}^{\rm T}x_u, \sum_{t\in I}\mathbf{V}^{\rm T}x_t \rangle \tag{18}
$$

Therefore, the FM mechansim can be viewed as a **table lookup** operation. The table is the second-order feature interaction matrix $V$. The lookup key is the user and item embeddings. To be more specific, recall the formula $(7)$, the ${\rm MatchScore}_{FM}$ can be viewed as the dot product of the user and item embeddings:

$$
{\rm MatchScore}_{FM} = \mathbf{E}_u \cdot \mathbf{E}_t \tag{19}
$$

where

$$
\begin{align*}
\mathbf{E}_u &= {\rm concat}(1, \sum_{u\in U}\mathbf{v}_u) \\
\mathbf{E}_t &= {\rm concat}(\mathbf{W}_t + \mathbf{V}_{tt}, \sum_{t\in I}\mathbf{v}_t)
\end{align*} \tag{20}
$$

where $\mathbf{E}_u$ represents user embedding that is calculated online, and $\mathbf{E}_t$ represents item emebedding that is calculated offline and stored in the sever to build the index. Note that $$\mathbf{W}_t + \mathbf{V}_{tt}$$ plays the significant role when $$\mathbf{V}_{ut}$$ cannot provide enough information, especially for new users.

As a result, the model is simplified to a shallow network where it solely calculates the multiplication of the user and item embeddings. This multiplication represents the click-through rate (CTR) estimation, indicating the likelihood of the user clicking on the item.

In recall (matching) tasks, once the model is trained, we obtain the user and item embeddings. Subsequently,we utilize the **approximate nearest neighbor (ANN)** algorithm to identify the nearest neighbors based on these embeddings. By leveraging these pre-trained embeddings, we can perform user-to-item (U2I) and item-to-item (I2I) recommendation tasks. Furthermore, these embeddings can also serve as input features for other more intricate tasks.

Indeed, FM can also be utilized in the ranking stage. FM shares similarities with subsequent DNN models that employ embeddings as inputs features. 

----
[^1]: [FM, 2010](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=5694074)

[^2]: [FM, FTRL, Softmax](http://castellanzhang.github.io/2016/10/16/fm_ftrl_softmax/)

[^3]: [FTRL](https://research.google.com/pubs/archive/41159.pdf)