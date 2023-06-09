---
title: Large Language Models
layout: default
nav_order: 5
---
# Large Language Models

TODO

## Timeline

| Model | Company | Cite | Date |
| --- | --- | --- | --- |
| Transformer | Google | 29k | 06/2017 |
| GPT | OpenAI | 3k | 06/2018 |
| BERT | Google | 27k | 10/2018 |
| GPT-2 | OpenAI | 5k | 02/2019 |
| GPT-3 | OpenAI | 3k | 05/2020 |


## GPT

[2018 OpenAI: Improving Language Understanding by Generative Pre-Training](https://cdn.openai.com/research-covers/language-unsupervised/language_understanding_paper.pdf)

<aside>
💡 semi-supervised learning = unsupervised pre-training + supervised fine-tuning = self-supervised learning

</aside>

## GPT-2

2019 OpenAI: Language Models are Unsupervised Multitask Learners

### Basic Info

- Dataset: WebText
- Parameter: 1.5B
- Zero-shot

## GPT-3

[2020 OpenAI: Language Models are Few-shot Learners](https://arxiv.org/pdf/2005.14165.pdf)

For all tasks, GPT-3 is applied without any gradient updates or fine-tuning, with tasks and few-shot demonstrations specified purely via text interaction with model GPT-3 achieves strong performance on many NLP datasets, including translation, question-answer, etc.

### Basic Info

- Parameter: 175B
- Information Retrieval: LSH, delete similar articles

## GPT-4

## InstructGPT

[2022 OpenAI: Training language models to follow instructions with human feedback](https://arxiv.org/abs/2203.02155)

## GPT4

## References
- **[CS324 - Large Language Models](https://stanford-cs324.github.io/winter2022/)**
The field of natural language processing (NLP) has been transformed by massive pre-trained language models. They form the basis of all state-of-the-art systems across a wide range of tasks and have shown an impressive ability to generate fluent text and perform few-shot learning. At the same time, these models are hard to understand and give rise to new ethical and scalability challenges. In this course, students will learn the fundamentals about the modeling, theory, ethics, and systems aspects of large language models, as well as gain hands-on experience working with them.
