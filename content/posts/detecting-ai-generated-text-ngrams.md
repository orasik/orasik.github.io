---
title: "How to detect AI generated text - Analysing n-grams"
date: 2024-09-06
categories: [ai,text,n-grams,nlp]
tags: [ai,text,n-grams,nlp]
description: "How to detect AI generated text? This is "
twitter: true
twitter_title: "How to detect AI generated text - Analysing n-grams"
twitter_image: "images/ai-generated-text-ngrams.jpg"
draft: True
---
Detecting AI generated text is becoming more important than ever and the use cases are endless. First examples come to mind is blog articles, academic papers, school assignments and so on.

There are many companies now offering services to detect AI content, and I got curious on how these companies are doing it. In the AI era, the fastest solution would be using multiple LLMs to identify if the text is AI generated or not, but how we can determine the accuracy?

So I decided to go back to basics and analyse AI vs Human generated text using NLP methods, and this post is about analysing n-gram frequency for AI vs Human content. This will be done by extracting bigrams, trigrams, and 4-grams for each content, and check the frequency (repetition) of these n-grams in the content.

The dataset used for this analysis is [DAIGT V2](https://www.kaggle.com/datasets/thedrcat/daigt-v2-train-dataset/data)

## TL;DR
1. Bigram frequency is almost the same for both AI and Human content.
2. More AI content has frequency of 3 or higher for trigrams.
3. More AI content has frequency of 3 or higher for 4-gram.
