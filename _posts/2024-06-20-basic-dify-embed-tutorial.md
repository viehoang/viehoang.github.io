---
title: Basic Dify Embed Tutorial
description: >-
  This article provides a step-by-step guide on how to include an iframe of Dify on your website. This is a great way to build a simple chatbot for your website.
date: 2024-06-20 23:00:00 +0900
categories: [Tools]
tags: [tools,tutorial]
published: true
---

## Create a pipeline

Dify offers a variety of pre-defined templates for your pipeline. To get started, click the "Create from template" button in the top-left corner of the application.

![Find creating template button](/images/2024-06-20/1.png)
_Figure 1: Locate the "Create from template" button in the top-left corner._

Next, from the list of templates, choose one that best suits your needs. In this example, we will build a RAG pipeline, so we select the "Knowledge Retrieval + Chatbot" template.

![Select Template](/images/2024-06-20/2.png)
_Figure 2: Select the "Knowledge Retrieval + Chatbot" template from the list._

You will then see an overview of your LLM pipeline.

![Pipeline overview](/images/2024-06-20/3.png)
_Figure 3: Overview of your LLM pipeline._

## Register a knowledge base 

For a RAG application, the knowledge base is crucial. Dify provides tools to streamline this process.

First, locate the knowledge tag at the top of the application.

![Where to find knowledge tag](/images/2024-06-20/4.png)
_Figure 4: Find the knowledge tag at the top of the application._

Depending on your plan, Dify offers different options for managing your knowledge base. Generally, there are three main options:

- Chunk settings:
    + *Automatic*: Predefined settings to split your long text into chunks.
    + *Custom*: Define Segment identifier, Maximum chunk length, and Chunk overlap yourself for greater flexibility based on your data.
- Index mode:
    + *High quality*: Uses in-house embedding created by Dify, but you must pay per token.
    + *Economical*: Free version using an offline vector engine, but the accuracy is not as high.
- Retrieval setting:
    + You can choose between vector search, full-text search, and hybrid search if you select the high-quality index mode.
    + Only inverted index is available if you select the economical index mode.

![Dify knowledge index options](/images/2024-06-20/8.png)
_Figure 5: Knowledge index options provided by Dify._

After creating the knowledge base, you can see how many chunks were created and test retrieval on your knowledge. For example, your PDF document might be split into 1796 chunks.

![Review your knowledge base](/images/2024-06-20/5.png)
_Figure 6: Review your knowledge base and see the number of chunks created._

## Publish the Pipeline

Once you have tested your pipeline, you can publish it as an embed version to add it to your site.

First, click the publish button in the top-right corner of the screen. Then, choose the embed into site option.

![Step to choose](/images/2024-06-20/6.png)
_Figure 7: Click the publish button and choose the embed into site option._

Dify supports three types of embed options for websites:

- Full screen
- Chatbox
- Dify Chatbot Chrome Extension

Choose the option that best fits your needs.

![Embed on site options](/images/2024-06-20/7.png)
_Figure 8: Embed options provided by Dify for websites._

The result of embedding on your site can look like this:

![Results](/images/2024-06-20/9.png)
_Figure 9: Example of the embedded Dify chatbot on a website._