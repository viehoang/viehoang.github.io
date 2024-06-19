---
title: Essential Prompting Techniques
description: >-
  In this article, I want to introduce to you some prompting techniques that can be used to improve the output of LLM.
date: 2024-06-18 23:00:00 +0900
categories: [Natural Language Processing, Prompting]
tags: [prompting,llm,techniques]
published: true
---

## Zero-shot Prompting
Zero-shot prompting involves asking a model to perform a task without providing any examples of the task in the prompt. This technique leverages the pre-trained knowledge of the model to generate responses based purely on the query.

Key Features:

- No Examples Provided: The model relies entirely on its training data.
- Versatile: Can be applied to a wide range of tasks, including translation, summarization, and question answering.
- Efficiency: Reduces the need for task-specific training data.

>**EXAMPLE**
>
I want to identify the dominant color of a painting based on its description. I will provide you with the description and your task is to help me classify it into the labels [red, blue, green].
>
Description: The sunset light glimmers on the sea.

## Few-shot Prompting
Few-shot prompting involves providing a model with a few examples of the task at hand within the prompt. This helps guide the model towards the expected output format and content.

Key Features:

- Contextual Guidance: Provides a few examples to help the model understand the task.
- Flexibility: Balances between zero-shot and fully supervised learning.
- Improved Accuracy: Typically results in more accurate responses than zero-shot prompting.

>**EXAMPLE**
>
>I want to identify the dominant color of a painting based on its description. I will provide you with the description and your task is to help me classify it into the labels [red, blue, green].
>
>Description: The sunset light glimmers on the sea.
>
><mark>
>Example 1: The sky is clear -> blue<br/>
>Example 2: I walk in the forest -> green<br/>
>Example 3: A flamingo is drinking water -> red
></mark>

## Revisit Role Prompting?

Revisit Role Prompting involves instructing a model to perform a task by explicitly assigning it a specific role or perspective to take during the task execution. This technique enhances the model's performance by guiding its behavior and responses based on the assigned role.

Key Features:

- Explicit Role Assignment: The model is given a clear role, such as a teacher, critic, or assistant, which influences how it generates responses.
- Enhanced Contextual Understanding: By taking on a specific role, the model can better tailor its answers to fit the expected tone and style associated with that role.
- Improved Coherence: Responses are more coherent and aligned with the assigned role, leading to higher quality and more contextually appropriate outputs.

>**EXAMPLE**
>
><mark>I want you to act as an astist.</mark>
I want to identify the dominant color of a painting based on its description. I will provide you with the description and your task is to help me classify it into the labels [red, blue, green].
>
Description: The sunset light glimmers on the sea.

## Chain-of-thought Prompting
Chain-of-thought (CoT) prompting encourages the model to generate a sequence of reasoning steps that lead to the final answer. This method helps in solving complex problems by breaking them down into smaller, manageable parts.

Key Features:

- Step-by-Step Reasoning: Guides the model to think through the problem.
- Enhanced Comprehension: Improves the model's ability to handle complex tasks.
- Transparent Process: Makes the reasoning process explicit.

There are two kind of CoT: Zero-shot CoT and Few-shot CoT

### Zero-shot CoT

This version of CoT doesn't explicitly tell models what to do. Instead, it adds the magic phrase "Let's think step by step" to encourage LLMs to articulate their reasoning process.


>**EXAMPLE**
>
>I want to identify the dominant color of a painting based on its description. I will provide you with the description and your task is to help me classify it into the labels [red, blue, green].
>
>Description: The sunset light glimmers on the sea.
>
><mark>
>Let's think step by step
></mark>


### Few-shot CoT

This type of CoT provides LLMs with an example of how to think, aiming for the models to replicate the process.



>**EXAMPLE**
>
>I want to identify the dominant color of a painting based on its description. I will provide you with the description and your task is to help me classify it into the labels [red, blue, green].
>
>Description: The sunset light glimmers on the sea.
>
><mark>
>Example: The sky is clear<br/>
>Chain-of-thought: <br/>
>&#45; Step 1: Understanding the Statement: The statement "The sky is clear" typically refers to a cloudless sky.<br/>
>&#45; Step 2: Visual Imagery: Imagine a clear sky in your mind — typically it's a bright blue color during the day.<br/>
>&#45; Step 3: Association with Color: The color associated with a clear sky is blue.<br/>
>Answer: blue
></mark>


## Least-To-Most Prompting
Least-to-most (LtM) prompting starts with simple prompts and gradually increases in complexity. This method helps the model build upon its previous responses and handle more complex tasks incrementally. 

Key Features:

- Incremental Complexity: Starts with easy tasks and progresses to harder ones.
- Building Blocks: Helps the model build a foundation before tackling complex problems.
- Stepwise Learning: Encourages a progressive learning approach.

From this prompting techniques, since LtM is used for complexity questions, we use a 3-hop one as an example.

> **Question**: Who was the US president when the latest Japanese emperor was born?\\
> **Correct Answer**: Dwight D. Eisenhower

![least-to-most-prompting](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fintermediate%2Fleast_to_most_formal.webp&w=1080&q=75)
_An overview of Least-To-Most Prompting_

To conduct LtM, we need two stages: Problem deduction and Sequentially solve sub-questions

### Problem Reduction

> Question: Who lived longer, Muhammad Ali or Alan Turing?\\
> Answer: To solve "Who lived longer, Muhammad Ali or Alan Turing?", we need to first solve: "How old was Muhammad Ali when he died?", then "How old was Alan Turing when he died?"
>
> Question: Who was the US president when the latest Japanese emperor was born? \\
> Answer:

### Sequentially solve sub-questions

In this stages, we asked the LLM all questions that being asked in the first stage and merge it with the original questions

## Self-Ask Prompting
Self-ask prompting involves the model generating sub-questions that it then answers to arrive at the final answer. This method encourages the model to break down the problem and self-direct its reasoning process. Details of self-ask prompting can be found [here](https://ofir.io/Self-ask-prompting/)

Key Features:

- Sub-question Generation: The model creates and answers intermediate questions.
- Autonomous Reasoning: Encourages the model to independently navigate through the problem.
- Enhanced Problem Solving: Improves the model's ability to handle complex queries by dissecting them.

> Try to answer the question in the same format as the example
>
><mark> 
Example:<br/>
Question: Who lived longer, Muhammad Ali or Alan Turing?<br/>
Are follow up questions needed here: Yes.<br/>
Follow up: How old was Muhammad Ali when he died?<br/>
Intermediate answer: Muhammad Ali was 74 years old when he died.<br/>
Follow up: How old was Alan Turing when he died?<br/>
Intermediate answer: Alan Turing was 41 years old when he died.<br/>
So the final answer is: Muhammad Ali 
></mark> 
>
>Question: Who was the US president when the latest Japanese emperor was born?\\
Are follow up questions needed here:


### Zero-shot self-ask

There is another one to implement self-ask prompting without have to find few-shot learning examples.

> <mark>Answer the following complex question by first breaking it down into sub-questions<br/>
So output:<br/>
Sub-question 1: ...<br/>
Answer to sub-question 1: ...<br/>
Sub-question 2: ...<br/>
Answer to sub-question 2: ...<br/>
So the final answer is: ...</mark>
>
Question: Who was the US president when the latest Japanese emperor was born?