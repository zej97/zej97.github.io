---
layout: default
title: "GPT-2: Zero-shot"
parent: Large Language Models
nav_order: 2
---

# GPT-2: Language Models are Unsupervised Multitask Learners

[2019 OpenAI: Language Models are Unsupervised Multitask Learners](https://d4mucfpksywv.cloudfront.net/better-language-models/language_models_are_unsupervised_multitask_learners.pdf)


## Introduction

GPT-2 is a significant advancement in the realm of language models, utilizing a **Transformer decoder** architecture with a staggering 1.5 billion parameters. It was trained on a vast dataset consisting of 8 million web pages. The training objective of GPT-2 is straightforward: predict the next word, based on all preceding words within a given text. The sheer diversity of the dataset contributes to this simple objective containing natural demonstrations of various tasks spanning diverse domains.

GPT-2 represents a direct scaling-up of its predecessor, GPT, with more than 10 times the number of parameters and trained on more than 10 times the volume of data. This increased scale enables GPT-2 to exhibit enhanced performance and a deeper understanding of language, facilitating its proficiency across a wide range of NLP tasks and domains.

## Basic Info

- Dataset: WebText
- Parameter: 1.5B
- Zero-shot