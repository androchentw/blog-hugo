---
title: "Auto-GPT & AgentGPT: Unleashing the Magic of AI-driven Task Completion - Get Started"
url: auto-gpt-agentgpt-introduction
# date: 2023-04-15T20:30:00+08:00
date: 2023-04-16T09:00:00+08:00
author: androchentw
type: post
categories:
  - tech
tags: 
  - aigc
  - chatgpt
  - autogpt
  - agentgpt
  - productivity
  - agile
share_img: https://github.com/androchentw/blog-hugo/blob/main/content/tech/aigc/2023-04-15-auto-gpt-agentgpt-introduction-1-architecture.en.png?raw=true
series: aigc
---

## Overview

<img style="width:100%;" src="https://github.com/androchentw/blog-hugo/blob/main/content/tech/aigc/2023-04-15-auto-gpt-agentgpt-introduction-1-architecture.en.png?raw=true">
<p align="center"><sub><sup>
  Auto-GPT / AgentGPT Autonomous AI Mechanism
</sup></sub></p>

Around 4 months after the release of ChatGPT, the [Auto-GPT](https://github.com/Torantulino/Auto-GPT) and [AgentGPT](https://agentgpt.reworkd.ai/) frameworks for AI-assisted task completion were introduced.

This means that by providing a "**Goal**," it can **automatically complete the task** through an iterative process of **breaking down the task, implementing, and verifying**.

The key to making Auto-GPT so powerful lies in:

1. 🧠 Utilizing LLM to understand requirements and initiate tasks
2. 🌐 Access to the internet for real-time updates
3. 💾 Support for long-term memory storage, overcoming ChatGPT token limits

Today, I will share some observations and let's discuss in 4 areas:

1. 🔥 Demonstration
2. ☠️ Warning: 💰 Budget control
3. 👀 Importance of requirements/review/stage evaluation
4. 🚀 Leverage Agile/Lean Startup "MVP" concept to build your own rocket

🤔 Q: To what extent can Auto-GPT achieve?

💪 A: Consider what you would use AI for, its effectiveness, and potential for further development.

> (2023/04/16) I'm an IT engineer from Taiwan 🇹🇼. I'm using ChatGPT and other software to help translate the original and future valuable articles. If there are any unclear expressions, please feel free to let me know. I'm also working hard to learn English and Japanese!

<!--more-->

## 🔥 Demonstration

<img style="width:80%;" src="https://github.com/androchentw/blog-hugo/blob/main/content/tech/aigc/2023-04-15-auto-gpt-agentgpt-introduction-2-agentgpt.png?raw=true">
<p align="center"><sub><sup>
  AgentGPT example Web UI
</sup></sub></p>

I used AgentGPT to ask, "Build a modern startup landing page," and it began to generate the following tasks automatically:

1. Generate a list of modern landing page designs from popular startup websites
2. Identify key design elements and features that are common among the selected designs
3. Create a prototype landing page incorporating the identified design elements and features

It then started with the first task, listing popular modern landing page designs like Airbnb, Uber, Spotify, etc. Although the details may not necessarily be what you initially wanted, it is a valuable reference for problem-solving approaches.

The vocabulary and steps used by Auto-GPT and AgentGPT differ slightly, but the essence is the same:

* Auto-GPT: Goal -> N Thought > (Reasoning, Criticism > Next Action, System) -> Result
* AgentGPT: Goal -> N Task > (Thinking > Executing) -> Result

<img style="width:80%;" src="https://github.com/androchentw/blog-hugo/blob/main/content/tech/aigc/2023-04-15-auto-gpt-agentgpt-introduction-3-auto-gpt.jpg?raw=true">
<p align="center"><sub><sup>
  Auto-GPT example command line interface
</sup></sub></p>

Also, [BabyAGI's Task-driven Autonomous Agent](https://twitter.com/yoheinakajima/status/1640934493489070080) has illustrated the principles, and I submitted a PR providing a [traditional Chinese translation](https://github.com/yoheinakajima/babyagi/blob/main/docs/README-zh-tw.md). Feel free to check it out if interested.

<img style="width:80%;" src="https://github.com/androchentw/blog-hugo/blob/main/content/tech/aigc/2023-04-15-auto-gpt-agentgpt-introduction-4-babyagi.png?raw=true">
<p align="center"><sub><sup>
  BabyAGI Architecture Principles
</sup></sub></p>

## ☠️ Warning: 💰 Budget control

One thing seems certain: Auto-GPT's continuous mode **will max out your credit card**.

So remember to set a budget limit on the OpenAI API.

## 👀 Importance of requirements/review/stage evaluation

<img style="width:80%;" src="https://github.com/androchentw/blog-hugo/blob/main/content/tech/aigc/2023-04-15-auto-gpt-agentgpt-introduction-5-programmer-joke.en.jpg?raw=true">
<p align="center"><sub><sup>
  Classic programming language joke - Buy 1 watermelon when you see it, buy 10 when you see oranges.
</sup></sub></p>

This reminds me of a classic programming language joke:

> Wife tells her husband, "Go to the supermarket and buy 1 watermelon if you see it, and buy 10 when you see oranges."
>
> In the end, the husband bought 10 watermelons.
>
> (Note: The husband "saw oranges" and bought 10 watermelons, but the wife's requirement was to buy 10 oranges)

As mentioned in the article "[6 Behavior Changes After 15 Weeks of AIGC Wave](https://blog.androchen.tw/6-behavior-change-after-AIGC-burst-15-weeks)" (sorry I haven't translate that at this moment), "**Precise questioning**" and "**Accurately describing requirements**" will become even more crucial in the future. This directly affects whether you'll end up with receiving 10 watermelons or other unexpected outcomes.

## 🚀 Leverage Agile/Lean Startup "MVP" concept to build your own rocket

<img style="width:100%;" src="https://github.com/androchentw/blog-hugo/blob/main/content/tech/aigc/2023-04-15-auto-gpt-agentgpt-introduction-6-mvp.jpg?raw=true">
<p align="center"><sub><sup>
  <a href="https://startupbasics.com/minimum-viable-product" target="_blank rel="noopener noreferrer">startup basics</a> - Lean Startup MVP concept: skateboard -> car
</sup></sub></p>

After reading the above, friends with experience in Agile software engineering should find it familiar.

**Avoiding spending lots of time and cost on building a product users don't need** is the strength of Agile and Lean Startup methodologies.

The so-called MVP refers to the **Minimum Viable Product**. Taking the skateboard and car as examples, it refers to the iterative approach when delivering a product to your key target customers:

* ❌ Shouldn't: Wheel > Chassis > Door > Car
* ✅ Should: Skateboard > Bicycle > Motorcycle > Car

The reason is straightforward: if your customer's pain point is "not wanting to walk and wanting a faster, more convenient mode of transportation," the skateboard might be delivered within two weeks. In contrast, a car's components cannot be delivered/used until fully assembled. By the time it's ready for use, possibly six months later, your customer's needs may have changed.

So perhaps we can utilize Auto-GPT on multiple levels. Here are some ideas:

1. Set MVPs, establish minimum goals in stages, evaluate results, and iterate repeatedly.
2. Learn how Auto-GPT breaks down tasks and use it in the typical Agile breakdown process: Epic > Story > Task.

## What do you think?

In the next article, I will share my hands-on experience and comparisons between Auto-GPT and AgentGPT.

What applications would you like to see?

Share your thoughts and let's discuss together! 🥳

### Murmur

* 2023-04-15: Astonishing development speed, truly the first year of the AIGC era. 🤣
