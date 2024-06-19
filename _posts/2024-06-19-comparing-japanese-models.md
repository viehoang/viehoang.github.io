---
title: Comparing Japanese LLMs using the same RAG-like prompt
description: >-
  Many large language models are specifically designed for Japanese, yet their performance remains uncertain. This article offers a simple visual comparison of these models.
date: 2024-06-19 23:00:00 +0900
categories: [Natural Language Processing, Large Language Models]
tags: [prompting,llm,techniques]
published: true
---

## Introduction

Large Language Models (LLMs) tailored for the Japanese language have become increasingly prevalent. Despite their proliferation, questions persist regarding their performance and effectiveness in various applications. This article aims to address these concerns by conducting a comparative analysis of several prominent Japanese LLMs. The comparison will be facilitated through the use of a consistent RAG-like prompt across all models, providing insights into their capabilities and limitations.

## Methodology

To ensure a fair evaluation, each LLM will be prompted with identical queries structured in a RAG-like format. This approach involves Retrieval-Augmented Generation (RAG), which integrates information retrieval into the generation process, thereby enhancing the model's ability to generate relevant and accurate responses.

## Prompt



### System Prompt

Japanese version of the system prompt

```
以下の文脈に基づいて質問に答えなさい。できるだけ多くの文脈を使い、できるだけ詳細に解答してください。
回答には、入力された質問内容を含めないこと。
提供された情報で答えられない場合は、次のように答えてください。
"申し訳ありませんが、情報がありません。"
```

English version of the system prompt

```
Answer the questions based on the following context. Use as much context as possible and provide as much detail as possible in your answer.
Do not include the question as typed in your answer.
If you cannot answer the question with the information provided, answer as follows.
"Sorry, we do not have the information."
```


### Query Format

For each run, we construct the query based on this format

```
Context: {context}

Question: {query}

Answer:
```

In which:

- Context: The specific context or topic that's relevant for understanding the application of RAG.
- Question: What is the specific question or prompt that the RAG system is addressing?
- Answer: Force models to output an answer based on the provided information

In this article, we only used one context to test all the models. The context is obtained from [the Wikipedia page on machine learning](https://ja.wikipedia.org/wiki/%E6%A9%9F%E6%A2%B0%E5%AD%A6%E7%BF%92) in Japanese. The context is:

*経験はなんらかのデータとしてプログラムに与えられる。このデータを訓練データもしくは学習データといい、売上予測タスクであれば例えば「過去の経験」である今日までの売上が訓練データとして与えられる。訓練データを使ってプログラムの性能を改善する過程を、「プログラムを訓練する」もしくは「プログラムを学習させる」という。またプログラムの訓練に用いられるデータ全体の集合を（訓練もしくは学習）データセット（データ集合とも）という。*

About the question, we use two kind of questions for our experiments

- Extracting information question
    + Question:
        - *データを使ってプログラムの性能を改善する過程は何と呼ばれますか？* 
        - What is the process of using training data to improve the performance of a program called?
    + Answer:
        - *「プログラムを訓練する」もしくは「プログラムを学習させる」* 
        - "training the program" or "teaching the program"

- Yes-no question
    + Question: 
        - *プログラムの訓練に用いられるデータ全体の集合をテストデータセットといいますか？* 
        - Is the entire set of data used for training a program called a test dataset?
    + Answer: 
        - *いいえ*
        - No

## Tested Models

In this article, we use LLMs that have demonstrated good performance, such as:

| Model                                             | JCommonsenseQA | JNLI | MARC-ja |
| ------------------------------------------------- | ----- | ----- | ----- |
| SakanaAI/EvoLLM-JP-v1-7B                          | 89.19 | 66.02 | 95.55 |
| SakanaAI/EvoLLM-JP-A-v1-7B                        | 86.68 | 62.13 | 92.12 |
| Rakuten/RakutenAI-7B-chat                         | 90.35	| 75.78 | 95.63 |
| Rakuten/RakutenAI-7B-instruct                     | 92.76 | 70.95 | 95.74 |
| stabilityai/japanese-stablelm-instruct-gamma-7b   | 91.42 | 40.73 | 72.94 |
| elyza/ELYZA-japanese-Llama-2-7b-instruct          | 79.18 | 38.80 | 89.94 |

# Results

## Extracting information question

| Model                                             | Correct? | Answer |
| ------------------------------------------------- | ----- | ---------- |
| SakanaAI/EvoLLM-JP-v1-7B                          | <i class="fa-regular fa-circle-check"></i> | データを使ってプログラムの性能を改善する過程は「プログラムを訓練する」もしくは「プログラムを学習させる」と呼ばれます。 |
| SakanaAI/EvoLLM-JP-A-v1-7B                        | <i class="fa-solid fa-xmark"></i> | データを使ってプログラムの性能を改善する過程は「訓練」と呼ばれます。 |
| Rakuten/RakutenAI-7B-instruct                     | <i class="fa-solid fa-xmark"></i>	| プログラムの訓練または学習と呼ばれます。 |
| Rakuten/RakutenAI-7B-chat                         | <i class="fa-solid fa-xmark"></i>	| 申し訳ありませんが、情報がありません。|
| stabilityai/japanese-stablelm-instruct-gamma-7b   | <i class="fa-regular fa-circle-check"></i> | データを使ってプログラムの性能を改善する過程は、「プログラムを訓練する」もしくは「プログラムを学習させる」という。 ... |
| elyza/ELYZA-japanese-Llama-2-7b-instruct          | <i class="fa-regular fa-circle-check"></i> | データを使ってプログラムの性能を改善する過程は、「プログラムを訓練する」もしくは「プログラムを学習させる」という。 |


## Yes-no question

| Model                                             | Correct? | Answer |
| ------------------------------------------------- | ----- | ---------- |
| SakanaAI/EvoLLM-JP-v1-7B                          | <i class="fa-solid fa-xmark"></i> |申し訳ありませんが、情報がありません。 |
| SakanaAI/EvoLLM-JP-A-v1-7B                        | <i class="fa-solid fa-xmark"></i> | 申し訳ありませんが、情報がありません。 |
| Rakuten/RakutenAI-7B-instruct                     | <i class="fa-solid fa-xmark"></i>	| 申し訳ありませんが、情報がありません。 |
| Rakuten/RakutenAI-7B-chat                         | <i class="fa-solid fa-xmark"></i>	| 申し訳ありませんが、情報がありません。 |
| stabilityai/japanese-stablelm-instruct-gamma-7b   | <i class="fa-regular fa-circle-check"></i>| データ全体の集合はデータセットといい、テストデータセットと呼ぶことはありません。|
| elyza/ELYZA-japanese-Llama-2-7b-instruct          | <i class="fa-solid fa-xmark"></i> | はい、いいます。 プログラムの訓練に用いられるデータ全体の集合は、学習データと呼ばれることもあります。 テストデータセットは、学習データを用いて訓練したプログラムの性能を検証するためのデータセットです。 よって、入力された質問に対する回答は以下となります。 回答: いいえ、いません。 |


## Findings

Surprisingly, from the results, we see that only *stabilityai/japanese-stablelm-instruct-gamma-7b* solved both problems correctly. *elyza/ELYZA-japanese-Llama-2-7b-instruct* only solved the yes-no question, meanwhile, *SakanaAI/EvoLLM-JP-v1-7B* only solved the information extraction question. Although *RakutenAI-7B-instruct* and *RakutenAI-7B-chat* have good benchmark scores, they could not solve any questions.

> Disclaimer: This could be due to incorrect use of the RakutenAI models since they have a different usage method compared to the other models.
{: .prompt-warning }

## Conclusion

In conclusion, this article provides a simple overview of Japanese LLMs through a structured comparative analysis. By employing a uniform RAG-like prompt methodology, we have shown an example of these models in use. As LLM technology continues to evolve, ongoing evaluations and advancements will be crucial in optimizing their performance for diverse applications in Japanese language processing.