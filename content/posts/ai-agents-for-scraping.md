---
title: "Can AI agents do scraping without guidance? Yes"
date: 2024-09-24
categories: [ai, agents]
tags: [ai, agents, llm]
description: "With agents able to run code safely now, I wanted to test their abilities to scrape data from websites without specifying any input requirements such as elements or classes. The result is shockingly good"
draft: false
---

# AI Agents for scraping.

With agents able to run code safely now, I wanted to test their abilities to scrape data from websites without specifying any input requirements such as elements or classes. The result is shockingly good, considering I spent less than 4 hours doing it.

## The challenge

- I didn't want to use a fully-fledged agent framework; I wanted to write one agent that would give feedback to itself if there were any errors to learn and iterate.
- I wanted to make a generic search term and expect the agent to understand it, write the code, run it, check the output, and iterate if there are any errors.
- I didn't want to implement function calling, as I wanted to test multiple LLMs without any limitations.

You can see the results in the video, I asked for tech gadgets on Amazon UK that are under £10, and got the right data.

## What did I learn

- Not all LLMs will give good results; I tried `DeepSeek coder`, `Llama 3 70B`, `Mixtral Instruct 22B` and `GPT-4o`. Only `GPT-4o` was able to run the code successfully in a few attempts. Others struggled to generate the correct code after 5 attempts.

- Running code in Docker will require setting up the correct Docker environment for your code. It's about generating the code and ensuring the environment has the required libraries and dependencies.

- I had to tweak the prompt to direct the LLM to the tech requirements. For instance, I asked to use Playwright, and after a few attempts, I noticed Chromium was getting timeout, so I added it to the prompt (always use Firefox).


All this with a single agent, having more agents to spec the requirements, doing QA, analysing output ... etc, would go a lot further.

{{< rawhtml >}} 

<video width=100% controls autoplay>
    <source src="/videos/AIScraper.mp4" type="video/webm">
    Your browser does not support the video tag.  
</video>

{{< /rawhtml >}}