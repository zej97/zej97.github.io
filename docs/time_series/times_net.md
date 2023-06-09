---
title: TimesNet
layout: default
parent: Time Series Prediction
nav_order: 1
---
# TimesNet

## Introduction

The latest research result from the *BNRist, Tsinghua University 2023*, [***TimesNet***](https://arxiv.org/pdf/2210.02186.pdf), is a temporal 2D-variation modeling method for general time series analysis. I realized this research matches my thought precisely at my first glance. 

From my perspective, it is essential to decouple different periods within a time series. It is widely recognized that even if some simple periodic functions can be integrated into a chaotic waveform. Therefore, decoupling different periods from a time series can substantially reduce the complexity for model to process. By doing so, the decoupled time series gains a clearer physical meaning, making it more interpretable not only for humans but also for algorithms. 

TimesNet is a general framework for time series analysis, including time series classification, time series clustering, time series forecasting, and time series anomaly detection. By transforming the 1D time series into a set of 2D tensors based on multiple periods, TimesNet breaks the limitation of the 1D time series and enables the model to capture the temporal 2D-variation of the time series.

## Methodology

Intuitively, Fast Fourier Transform (FFT) is a natural choice for decoupling different periods from a time series. 

Assume the time series is $$\mathbf{X}_{\rm 1D} = \lbrace \mathbf{x}_1, \cdots, \mathbf{x}_T\rbrace$$, where $$T$$ denotes the length of the time series. Each element $$\mathbf{x}_t$$ records $$C$$ variates. Therefore, the original $$\rm 1D$$ organization is $$\mathbf{X}_{\rm 1D} \in \mathbb{R}^{T\times C}$$. Then our first step is to extract the periodical functions from the time series:

$$
\begin{align*}
&\mathbf{A} = {\rm Avg\left(Amp\left(FFT(\mathbf{X}_{1D})\right)\right)}, \\[10pt]
&\lbrace f_1, \cdots, f_k\rbrace = \mathop{\rm argTopk}\limits_{f_\ast\in\lbrace 1, \cdots, [\frac{T}{2}]\rbrace}{(\mathbf{A})},\\
&p_i = \lceil \frac{T}{f_i} \rceil, \quad i \in \lbrace 1, \cdots, k, \rbrace \\
\end{align*} \tag{1}
$$

Here, 

1. $\rm FFT(\cdot)$ denote the Fast Fourier Transform, $\rm Amp(\cdot)$ denotes the amplitude of different periodical functions. 
2. $\mathbf{A} \in \mathbb{R}^{T}$ denotes the amplitude of each frequency, which is average from $C$ dimensions by $\rm Avg(\cdot)$. 
3. $\rm argTopk(\cdot)$ represents that we only select the frequencies of the top $k$ amplitudes in $\mathbf{A}$ to avoid the noises brought by meaningless high frequencies. 
4. $f_i$ denotes the frequency of the $i$-th periodical function. $p_i$ denotes the period length of the $i$-th periodical function.


TODO