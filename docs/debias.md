---
layout: default
title: Debias
parent: Recommendation System
nav_order: 2
---
# De Position Bias
## Background
Ideally, we want users' click behavior to align with their actual preferences. However, in reality, their click behavior is often influenced by various factors such as the position, freshness, and popularity. These factors result in bias, where users' click behavior deviates from their actual preferences. I.e., if a user doesn't click on an item, it doesn't mean that he doesn't like it. In contrast, if a user clicks on an item, it doesn't mean that he likes it.
Bias affects the accuracy of recommendation systems, so debiasing the data is necessary to improve the system's accuracy. In this paper, I will introduce the methods I used to debias the position bias while working at ByteDance. Debiasing is always a challenging problem in the industry, as it is difficult to evaluate the performance of debiasing algorithms.

### Position Bias
Position bias is the most common bias in recommendation systems. It arises from the fact that users are more likely to click on items that are displayed in a more prominent position. Our investigation reveals that even when two items have the same ranking score, the item in the first position is more likely to be clicked. Therefore, the data we collect from the real world is biased. However, we often fail to account for this bias when training our model, which results in a model that is biased towards the first position. To address this issue, we need to introduce a debiasing mechanism into our model.

## Debiasing Mechanism
There are three ways to introduce a debiasing mechanism into our model. The first is to use item position in each session as a feature when training the model. Since we don't know the actual position of the item in when serving, we set every item's position to a same value e.g. 0. Then we use our model to predict scores with this dummy position. The second approach is to model the position bias separately, and only use the ranking model when serving. This method avoids the problem of dummy position (explained below). The third approach is inverse propensity weighting (IPW)[^1].

<img style="float: right;" src="../assets/images/base_feature.png"  width="60%" height="60%">

The first approach is the simplest, but it has a major problem. The position feature will inevitably interfere with the model's learning of other features due to its interaction with other features when training NN model. Therefore, if we mask the position feature when serving, the cross feature will be different from the training phase, which will affect the model's performance. That's why I prefer to use a separate shallow tower to model the position bias. 

It would be convenient for us to analyze the effect of position if we decouple the position bias from the ranking model. We use a shallow tower to avoid over-generalization and increase memory capacity (the key concept of Wide&Deep[^2] structure).

### YouTube[^3]
<img style="float: right;" src="../assets/images/youtube_debias.png"  width="60%" height="60%">

The figure right illustrates the structure of YouTube's debiasing mechanism. The position bias is modeled by a shallow tower, which consists of a fully connected layer with a sigmoid activation function. The input of the shallow tower is the position of the item in the session, and its output is the position bias.

The ranking model is a deep tower, with the user's click history and the candidate item's features as inputs. **The output of the deep tower is the ranking score, which is added to the position bias to obtain the final score.** The final score is then used to rank the items.

### HuaWei: PAL[^4]
<img style="float: right;" src="../assets/images/pal.png" width="60%" height="60%">

The main difference between PAL and YouTube is that PAL **multiplies** the position bias with the ranking score instead of adding them together. 

Our model is similar to PAL. The ranking model aligns with the online model we were using. The position bias is modeled by a simple shallow tower, i.e., a single-layer neural network.

To implement this shallow model, I need to introduce a new feature: the absolute position of an item in a session. The absolute position is the position of an item in the entire session. For example, if a session contains 10 items, the absolute position of the first item is 1, and the absolute position of the last item is 10. The absolute position serves as the input of the shallow tower. The output of the shallow tower is the representation of the position bias. The position bias is then multiplied with the ranking score to obtain the final score:

$$
{\rm final\_score = ranking\_score \times position\_bias} = {\rm DNN}(u, t) \times w^\top b
$$

where $\rm DNN$ is the ranking model, $u$ is the user's features, $t$ is the candidate item's features, $w$ is the weight of the shallow tower, and $b$ is the position bias.



(Todo: the difference between relative position and absolute position).

## Conclusion
This model has a gain of almost 0.2% for the xxx.

---

[^1]: [Unbiased Learning to Rank with Unbiased Propensity Estimation](https://arxiv.org/pdf/1804.05938.pdf)

[^2]: [Wide & Deep Learning for Recommender Systems](https://arxiv.org/pdf/1606.07792.pdf)

[^3]: [Recommending What Video to Watch Next: A Multitask Ranking System](https://daiwk.github.io/assets/youtube-multitask.pdf)

[^4]: [PAL: a position-bias aware learning framework for CTR prediction in live recommender systems](https://dl.acm.org/doi/10.1145/3298689.3347033)
