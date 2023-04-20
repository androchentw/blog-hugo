---
title: "3-Minute Infographic - Boost Productivity with ChatGPT + Mermaid"
url: 3-minute-infographic-chatgpt-mermaid-productivity
# date: 2023-04-19T22:00:00+08:00
date: 2023-04-20T10:00:00+08:00
author: androchentw
type: post
categories:
  - soft
tags: 
  - aigc
  - chatgpt
  - productivity
  - infographic
  - diagram
share_img: https://github.com/androchentw/blog-hugo/blob/master/content/soft/productivity/2023-04-20-3-minute-infographic-chatgpt-mermaid-productivity-cover.en.png?raw=true
series: productivity
---

## Overview

<img style="width:60%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/soft/productivity/2023-04-20-3-minute-infographic-chatgpt-mermaid-productivity-cover.en.png?raw=true">
<p align="center"><sub><sup>
  3-Minute Infographic - Boost Productivity with ChatGPT + Mermaid
</sup></sub></p>

Today I'd like to share the diagramming tools I use in practice and how I combine them, hoping to help friends who love using visualization to illustrate their logic.

Actually, diagram-as-code tools have been around for a while; it's just that ChatGPT makes this task even easier.

Features of today's introduced tool:

1. 🌐 Free to use on a web page.
2. 🚀 Quickly generate flowcharts, mindmaps, pie charts, Gantt charts, timelines, user journeys, and more.
3. 📝 Uses markdown syntax, easy to learn even without an engineering background, convenient for version control.

<!--more-->

## What is Mermaid

> JavaScript based diagramming and charting tool that renders Markdown-inspired text definitions to create and modify diagrams dynamically.

The official website directly provides an online editor called [Mermaid Live Editor](https://mermaid.live).

The [Mermaid official tutorial documentation](https://mermaid.js.org/syntax/flowchart.html) offers a variety of syntax examples to refer to. Approximately 15 types of charts can be drawn, divided into two categories below:

### 1. Flowchart

```md
flowchart LR

A[Hard] -->|Text| B(Round)
B --> C{Decision}
C -->|One| D[Result 1]
C -->|Two| E[Result 2]
```

{{< mermaid >}}
flowchart LR

A[Hard] -->|Text| B(Round)
B --> C{Decision}
C -->|One| D[Result 1]
C -->|Two| E[Result 2]
{{< /mermaid >}}

### 2. Timeline

```md
timeline
    title History of Social Media Platform
    2002 : LinkedIn
    2004 : Facebook
         : Google
    2005 : Youtube
    2006 : Twitter
```

{{< mermaid >}}
timeline
    title History of Social Media Platform
    2002 : LinkedIn
    2004 : Facebook
         : Google
    2005 : Youtube
    2006 : Twitter
{{< /mermaid >}}

### 3. Gantt

```md
gantt
    section Section
    Completed :done,    des1, 2014-01-06,2014-01-08
    Active        :active,  des2, 2014-01-07, 3d
    Parallel 1   :         des3, after des1, 1d
    Parallel 2   :         des4, after des1, 1d
    Parallel 3   :         des5, after des3, 1d
    Parallel 4   :         des6, after des4, 1d
```

{{< mermaid >}}
gantt
    section Section
    Completed :done,    des1, 2014-01-06,2014-01-08
    Active        :active,  des2, 2014-01-07, 3d
    Parallel 1   :         des3, after des1, 1d
    Parallel 2   :         des4, after des1, 1d
    Parallel 3   :         des5, after des3, 1d
    Parallel 4   :         des6, after des4, 1d
{{< /mermaid >}}

### 4. Pie chart

```md
pie title Pets adopted by volunteers
    "Dogs" : 386
    "Cats" : 85
    "Rats" : 15
```

{{< mermaid >}}
pie title Pets adopted by volunteers
    "Dogs" : 386
    "Cats" : 85
    "Rats" : 15
{{< /mermaid >}}

### 5. User Journey

```md
journey
  title My working day
  section Go to work
    Make tea: 5: Me
    Go upstairs: 3: Me
    Do work: 1: Me, Cat
  section Go home
    Go downstairs: 5: Me
    Sit down: 3: Me
```

{{< mermaid >}}
journey
  title My working day
  section Go to work
    Make tea: 5: Me
    Go upstairs: 3: Me
    Do work: 1: Me, Cat
  section Go home
    Go downstairs: 5: Me
    Sit down: 3: Me
{{< /mermaid >}}

### 6. Mindmaps

Since I'm not used to using radial mind maps, I use [Markmap](https://markmap.js.org/repl) to generate mindmaps.

### Other engineering-related tools

Please refer to the [official documentation](https://mermaid.js.org/syntax/flowchart.html) for the following:

1. Sequence Diagram
2. Class Diagram
3. State Diagram
4. Entity-Relationship (ER) Diagram
5. 🔥 Gitgraph
6. C4C diagram

## Practical Applications of ChatGPT + Mermaid

You might wonder that the Mermaid markdown syntax still looks a bit complicated. That's right! That's why we let ChatGPT help us generate the syntax templates. It's recommended to choose tasks that ChatGPT is good at, such as generating, summarizing, translating, and so on.

In my example, using a Markmap mind map is more convenient, and Mermaid follows the same principle. So, we can achieve the following things in just 3 minutes:

1. 🤖 [ChatGPT](https://chat.openai.com/): ChatGPT: Use a Prompt to generate the needed content
2. 📝 [Mermaid Live Editor](https://mermaid.live/): Directly input the content into Mermaid to generate the chart
3. 🎉 Done!

For example, if you want to summarize this article, you can use the following Prompt:

```md
# ChatGPT prompt for markdown
provide summary in bullet point and in markdown codeblock:

# ChatGPT prompt for Mermaid
provide summary mermaid diagram in markdown codeblock:
```

Get the markdown below:

```md
- Overview
- What is Mermaid
    1. Flowchart
    2. Timeline
    3. Gantt
    4. Pie chart
    5. User Journey
    6. Mindmaps
    7. Others
- Practical Applications of ChatGPT + Mermaid
- Other Tools
- Your Thoughts?
```

Paste it into [Markmap](https://markmap.js.org/repl) to generate the mind map, which becomes the cover image of this article.

The Mermaid version uses a flowchart, which is more my style:

```md
graph LR
    A[Overview] --> B[What is Mermaid];
    B --> C[Flowchart];
    B --> D[Timeline];
    B --> E[Gantt];
    B --> F[Pie chart];
    B --> G[User Journey];
    B --> H[Mindmaps];
    B --> I[Others];
    A --> J[Practical Applications of ChatGPT + Mermaid];
    A --> K[Other Tools];
    A --> L[Your Thoughts?];
```

{{< mermaid >}}
graph LR
    A[Overview] --> B[What is Mermaid];
    B --> C[Flowchart];
    B --> D[Timeline];
    B --> E[Gantt];
    B --> F[Pie chart];
    B --> G[User Journey];
    B --> H[Mindmaps];
    B --> I[Others];
    A --> J[Practical Applications of ChatGPT + Mermaid];
    A --> K[Other Tools];
    A --> L[Your Thoughts?];
{{< /mermaid >}}

By the way, I don't know why the Mermaid results generated by GPT-3.5 are better than those by GPT-4. If you have any experience, feel free to leave a comment and share~

## Other tools

1. [Miro](https://miro.com/): When I want to draw more highly customized block diagrams or other charts, I prioritize Miro. I love the large whiteboard, where I can put many draft ideas together with the final version.
2. [diagrams.net (formerly known as draw.io)](https://app.diagrams.net/): The charting tool is actually renamed to diagrams.net, but everyone still calls it Draw.io. Its advantage lies in having many built-in components when drawing complete architecture diagrams. But aligning the components by dragging them can be quite painful...
3. [Excalidraw](https://excalidraw.com/): A hand-drawn-style charting tool. I used it for a while before switching to Miro.
4. [PlantUML](https://plantuml.com/): A tool often compared to Mermaid. It has a more classic interface. I used it in the past, but not so much now.
5. VS Code Plugin
   1. [Markdown Preview Mermaid Support](https://marketplace.visualstudio.com/items?itemName=bierner.markdown-mermaid)
   2. [Markmap](https://marketplace.visualstudio.com/items?itemName=gera2ld.markmap-vscode)

## What do you think?

Let's discuss thoughts together! 🥳

### Murmur

* 2023-04-22: Everything as Code belief 🤣
