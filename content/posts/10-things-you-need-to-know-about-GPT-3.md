---
title: "In the waiting list for OpenAI? here are 10 things you should know about GPT-3"
date: 2021-01-22
categories: [gpt-3]
tags: [gpt-3]
description: "if you are new to OpenAI GPT-3, here is a 10 things you should know about it to manage your expectations and know the limits"
draft: false
---

## In the waiting list for OpenAI? here are 10 things you should know about GPT-3

I have received my invitation to OpenAI at the end of Nov and started playing around with API two weeks after that. I will list the top 10 things I didn't know or didn't expect as a newcomer to the GPT-3.

## TL;DR

If you don't like long details, here is a TL;DR:

1. OpenAI is not one text generation engine. There are multiple engines, and they differ in terms of speed and accuracy.
2. Choosing the most accurate engine can be very expensive, depending on your use case.
3. Getting the optimum result is not an easy task; you will need to try and error and adjust some parameters.
4. Integration with open ai is fairly simple.
5. You cannot go live immediately, you need open ai team approval.
6. The safety of the generated text safety is your responsibility.
7. There is a slack channel to ask questions and learn from each other's and the support team reply to people directly.
8. You cannot make apps that send automatically to social media without a human in the middle.
9. You cannot make apps that generate content for medical purposes or political influence.
10. There are lots of improvements going on, so this list might change over time ;)

### 1. OpenAI is not one text generation engine.

Once you have your account, you'll be introduced to the playground where you can start generating text based on prompts (text input). This might sound complicated, but here is a simple example:
OpenAI is a text-in/text-out engine. You provide your prompt (text input), and it will generate text to match the context.
There are some examples and videos to show you how you can use the playground and how to tune the parameters.

### 2. Choosing the most accurate engine can be very expensive.

At the time of writing this blog, The most accurate engine is called `DaVinci`. While it would appeal that everyone should use, practically this is not the case mainly due to the price.

`Davinci` is 10 times more expensive than the next engine `curie` and at the moment you get charged by the number of tokens sent/received from the API. These tokens include your prompt.

So for instance, if you're creating a chat service where you keep appending to your initial prompt, your cost will increase with each call to the API.

If you want to have an idea about how tokens are being calculated, you can check this tool:
[GPT Tools](https://www.gpttools.com)

### 3. Getting the optimum result is not an easy task.

You will have to adjust parameters, change your prompt, try different scenarios, and you will get there eventually. This is not to say it is very hard or impossible, expect there will be some work from your side to ensure you're providing the right context in your prompt.
The documentation has excellent examples to show you how to do the following:

- Summarization.
- Classification.
- Idea Generator.

### 4. The integration with open ai fairly simple.

This blog is aimed for developers, and in this context, the integration with OpenAI API is fairly simple. In the playground, you'll have an export button to export your prompt to either `cURL` or `Python` code, but in the documentation, you will find various community libraries including:

- C#/ASP.NET
- Go lang.
- Dart.
- Java.
- Node.
- Ruby.

### 5. You cannot go live immediately.

Now that you managed to make the perfect prompt design for your app and started generating the expected results, there is still another step to do before going live, and that is the approval of the OpenAI team.

This review process ensures the safety of the generated text and that users will not misuse your app to generate harmful or offensive materials.

In my experience, it took 8 days to get the approval for my app [Job Description](https://jobdescription.ai).

You'll have to fill a lengthy form explaining your idea, which part of your app is GPT-3 based and which part is a human-based.
You will also need to provide a short video of your app to show the functionality.

### 6. The safety of the generated text safety is your responsibility.

Following point 5, the safety of the generated text is your responsibility. It would be best if you made sure that the output is not offensive or harmful.
There are multiple ways to ensure that one of them uses filters in the API itself, and another one is to use a library on your side to filter inputs and outputs.

One of these libraries is [Bad Word](https://github.com/web-mech/badwords#readme)

### 7. There is a slack channel to ask questions and learn from each other's and the support team reply to people directly.

By now, you might think that this is overwhelming, but the reality is `you are not alone`. There is a slack channel for members where you can ask questions, share ideas, ask the support team and even share your app when you're ready to go live.

### 8. You cannot make apps that send automatically to social media without a human in the middle.

If you are thinking of creating a bot that will generate social media posts, I'm sorry to be the party popper. This is not allowed, and it's against the OpenAI rules. But if you are going to generate ideas, titles, and a short description used by a human to post to social media than this is fine.

### 9. You cannot make apps that generate content to diagnose medical or psychiatric conditions or political influence.

There is also a list of high-risk domains that will be hard to get approval. These are available in the FAQ section when you join in.

### 10. There are lots of improvements going on, so this list might change over time ;)

In my short time as a member, there were lots of improvements. The OpenAI team have added safety measures best practices list to help developers ensure their apps are safe. The team is also working on some enhancements to speed up the approval process, and the first step was introducing the lengthy form mentioned in point 5.

That's all if you have feedback or questions, please reach out at [@orask][https://www.twitter.com/orask]
