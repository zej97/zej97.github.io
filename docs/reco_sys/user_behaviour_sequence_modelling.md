---
layout: default
title: User Behavior Sequence Modeling
parent: Recommendation System
nav_order: 4
---
# Ranking Models: User Behavior Sequence Modeling
## Introduction

Traditional recommendation systems only have the ability to capture general user preferences and represent user-item interaction in a static way. In reality, however, the user interests in recommendation systems are dynamic in nature with a strong correlation and even causality between the actions of users, i.e., how previous behaviours affect subsequent behaviours. Moreover, users always have multiple interests, and the importance of these interests not only varies through time but also depends on the candidate items. For example, a user may be interested in both sports and music, but the user's interest in sports may be more important when the user is browsing sports news, while the user's interest in music may be more important when the user is browsing music news. There are so many valuable features in the user behaviour sequence that can be used to improve the performance of the recommendation system. Therefore, the industry faces a new challenge: how to model a user behaviour sequence. 

## Attention-based Models

Attention is one of the most widely used mechanisms in deep learning. It was first proposed in the field of natural language processing (NLP) and has been widely used in many fields such as computer vision and recommendation systems. The standard attention is defined as:

$$
\begin{align*}
    {\rm Attention}(\mathbf{Q, K, V}) = {\rm softmax}(\frac{\mathbf{QK}^T}{\sqrt{d_k}}){\mathbf{V}}
\end{align*}
$$

here $\mathbf{Q}$ is the query vector, $\mathbf{K}$ is the key vectors, $\mathbf{V}$ is the value vectors, and $d_k$ is the dimension of the key vectors. Specifically, self-attention uses the same objects as queries, keys, and values. In self-attention, the model assigns a weight to each input element and uses these weights to calculate a weighted sum of the input elements. The weights are learned during training and are used to determine which input elements are most relevant to the task.

The introduction of the **attention score** reflects the natural **attention mechanism** characteristic of humans. The simulation of this mechanism allows recommendation systems to be closer to the real thinking process of a user, i.e., "paying attention " to certain parts of the input when making decisions, thus improving the effectiveness of recommendations.

In 2017, Attentional Factorization Machines (AFM) introduced the attention mechanism to the traditional recommendation model FM\cite{FM}. In August 2018, Kang and McAuley released Self-Attentive Sequential Recommendation model (SASRec). In September of the same year, Zhou et al. proposed Deep Interest Network (DIN). Both models are deep learning-based, incorporating the attention mechanism. Compared with the FM-based AFM model, the DIN model is a more typical attempt to improve deep learning networks, and it also gives more substantial inspiration to recommendation engineers because the starting point is a specific business scenario.

### Deep Interest Network (DIN)

<center><img style="margin: 20px;" src="../../assets/images/DIN.png"></center>

For different candidate items, most traditional CTR prediction models such as always map the sequence of the user's historical behaviour to the same fixed-length vector, but this greatly limits the expressiveness of the features. In order to address this issue, the DIN will evaluate the similarity between a user historical behaviour sequence with different candidate objects via self-attention, and then it will extract various interest features in an adaptive manner.

### Deep Interest Evolution Network (DIEN)

<center><img style="margin: 20px;" src="../../assets/images/DIEN.png"></center>

After DIN was proposed, Zhou et al. released its upgraded version, Deep Interest Evolution Network (DIEN), in 2019. The innovation lies in the use of a sequence model AUGRU to simulate the evolution of the user's interests. Both AFM and DIN simply score the relevance of different actions, such that the scores are time-independent, or sequence-independent. However, models will not be as effective at learning about time and trends if sequential information is removed. Instead of recommending for "next behaviour," the recommendation model would continue to be based on an analysis of all the user's past behaviour. This is the flaw that was emphasised as having to be fixed in the earlier section.

To be specific, as shown in Figure, the key components of the model are the interest extractor layer, which generates interest, and the interest evolving layer, which simulates interest evolution, between the embedding layer and the concatenate layer. The interest extractor layer uses the structure of DIN to extract the interests of users at each time $t$, while the interest evolving layer uses the structure of the sequence model AUGRU to link the interests of users at different times to form a chain of interest evolution. The interest vector at the current moment is then fed into the upper layer of the multi-layer fully-connected network, together with other features, for the final CTR prediction.
### Search-based User Interest Modelling (SIM)

<center><img style="margin: 20px;" src="../../assets/images/SIM.png"></center>

Industry experts are gradually coming to the consensus that the more detailed the user behaviour data, the more useful it is for model prediction. Notwithstanding, longer user historical behaviour sequences provide more information for user interest modelling, but they place a significant load on an online serving system's latency and storage. Consequently, the majority of proposed techniques can only model sequential user behaviour data with length scaling up to hundreds. To tackle this problem, Pi et al. designed a new modelling paradigm SIM (Search-based User Interest modelling) based on DIEN in 2020. It extends the maximum length for modelling user behaviour sequences up to $54,000$, which is significant increase over MIMN, the released state-of-the-art industry solution for this work in 2020.

To solve the performance problem caused by very long user behaviour sequences, SIM divides the search of the full sequence of candidate items into two phases, namely GSU (General Search Unit) and ESU (Exact Search Unit). 

Pi et al. indicate that only some user behaviours, given a certain candidate item, are valuable. The final user decision is closely tied to this portion of the user's past actions. In the first stage, as shown in Figure, GSU picks out these relative user behaviours to reduce the number of user historical behaviours that need to be processed. In the second stage, ESU uses multi-head attention to extract users' varied interests. After that, it adopts the conventional Embedding & MLP paradigm, which uses other features such as user profiles and context features as inputs.

These three models from Alibaba are important in terms of application and serve as an example of the work that has been done recently in the industry. From DIN to SIM, Alibaba has made solid and practical breakthroughs in each case, building on its previous model. The technical evolution of Alibaba's recommendation model is very informative. At present, companies like ByteDance and Kwai have developed their recommendation models based on the SIM, and have achieved significant success. However, given the large data scale in the industry, soft search requires a higher level of computing resources, which may be unacceptably expensive.