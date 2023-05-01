# ChatGPT Language Learning: 6 Tips for Utilizing YouTube + Free Plugins to Improve TOEIC Score

## Overview

I have been actively using ChatGPT to self-study English and Japanese recently.

Features of the tools introduced today:

1. 🌐 Free to use online.
2. 🚀 Generate bilingual subtitles and video summary Mindmap on YouTube with one click and convert them into TOEIC test questions.
3. 📝 Combine ChatGPT translation and modification features to create your vocabulary book and essay collection.

🤔 Q: How would you use ChatGPT to assist with language learning?

💪 A: Choose a YouTube video and generate video summaries and TOEIC learning content in practice.

> (2023/05/01) I'm an IT engineer from Taiwan 🇹🇼. I'm using ChatGPT and other software to help translate the original and future valuable articles. If there are any unclear expressions, please feel free to let me know. I'm also working hard to learn English and Japanese!

## 1. YouTube Online Free Audiovisual Teaching Materials

1. TED-Ed: A well-known educational content sharing platform with many practical content.
2. BBC Learning English: Free English lessons from BBC.
3. ESL Brains: Video materials designed for adults. My online tutor uses this for classes. Teacher and student PDFs are available for download.

Today, I mainly choose this video from ESL Brains to demonstrate: You're never too old for great things

## 2. Trancy Bilingual Subtitles + Immersive Learning

Trancy is a browser extension with the following features:

1. Convert YouTube transcripts into bilingual subtitles
2. Provide vocabulary examples
3. Additional online assistant features on web pages

It is perfect for **Shadowing** to train listening and speaking skills comprehensively along with the video content.

## 3. Glarity Video Summary + TOEIC Questions + Vocabulary List

Next is today's highlight, Glarity, another browser extension. Its main features are:

1. Video / web page search results summary
2. Translation

However, since Glarity's settings page allows custom prompts, we can freely transform any YouTube video into TOEIC test material:

1. TOEIC listening questions / answers. You can specify how many questions you want.
2. TOEIC writing summary / opinion. You can specify the number of words and proportion of the composition.
3. Select 10 vocabulary words, generate definitions, synonyms, antonyms, and bilingual example sentences.

In the TOEIC writing section, I specified using 100 words and composing with a 30% summary / 70% opinion ratio. This is because I feel my weaker area is discussing viewpoints like "**what I see from this video**," so I chose this ratio. I also share the prompt I used below:

```prompt
Output should use the following template:
### Summary
- [Emoji] bullet point
### TOEIC Listening Questions
### TOEIC Listening Answers
### TOEIC Writing Answers
#### Summary
#### Opinion
### Vocabulary

Use up to 5 brief bullet points to summarize the content below, Choose an appropriate emoji for each bullet point. 
Provide 3 TOEIC listening questions with answers.
Provide TOEIC writing answers, with 30% summary and 70% opinion in around 100 words.
Choose 10 vocabulary words and provide definitions, synonyms, antonyms, and sentence examples.
: {{Title}} {{Transcript}}.
```

### One-click Copy to Generate Mindmap

Glarity also has a feature I like, which is the ability to copy the entire answer with one click while retaining the markdown format. If you're quick-witted, you'll know you can use markmap or mermaid to draw mindmaps like below.

For detailed operation, please refer to my previous article: [3-Minute Infographic - Boost Productivity with ChatGPT + Mermaid](https://blog.androchen.tw/en/3-minute-infographic-chatgpt-mermaid-productivity/)

## 4. ChatGPT Translation, Creating Vocabulary Lists


As for the vocabulary generated during the learning process, I use **ChatGPT as a translation tool**. Ever since I had ChatGPT, I rarely use Google Translate 😂

Use the following prompt and replace `<vocabulary>` with the word, and ChatGPT will provide **definitions, synonyms, antonyms, and bilingual example sentences**:

```prompt
1. Provide definitions, synonyms, antonyms, and sentence examples in English and respond in markdown code block
2. Translate to Traditional Chinese

<vocabulary>
```

Because ChatGPT saves previous records, I use the same prompt directly, replacing the part I want to look up. This saves the trouble of finding the prompt each time, and you can **switch left and right** to view unfamiliar vocabulary, turning ChatGPT into a vocabulary list!

I highly recommend learning through example sentences, reading them several times to strengthen memory, and the key is to know **how to apply**. Prompts are flexible, so you can continue to expand and add your own content. Or adjust the format, like I especially like markdown syntax, so the example above also asked ChatGPT to change the content of the answer into markdown format, making it easy for me to copy and paste.

## 5. ChatGPT Essay Editing, Building Your Own Essay Library

Next, we can use ChatGPT to help us edit our essays.

For example, we've already used Glarity to help us write an essay. Now it's our turn to write and then ask ChatGPT to help correct it and point out errors. I won't demo this specifically here, but I'll provide some directions for reference:

1. **Grammar checking and explanation**
2. **Polishing** for a more concise/smooth expression

```prompt
1. Check the grammar in my essay and suggest any corrections if necessary.
2. Rephrase any parts of my essay that could be written more effectively or concisely.
```

## 6. Begin with the End in Mind + Continuous Measurement

Finally, I want to share a learning tip with you: I recommend setting goals by "**beginning with the end in mind**." **First imagine what level you want to reach, and then work backward to determine what actions you should take**.

For example, if you want to memorize 3,000 words in 30 days, working backward means you need to progress at a rate of 100 words per day. The same concept is mentioned in the book "The 7 Habits of Highly Effective People":

> Begin with the end in mind.

In addition, "**continuous measurement**" is also crucial. You just need to take your own speed seriously, without comparing yourself to others.

For example, if you initially set the goal of "writing a 200-word essay every day with 1 hour of practice," but after a week you find it takes 2 hours to complete the entire learning process, simply record it honestly and adjust accordingly.

For those who have been following my articles, you might feel that I mention "**agile mindset, continuous output**" a bit too much. But I truly believe in it and practice it myself. It's the agile mindset of continuous output that supports me to keep writing and sharing the concept of an agile life again 😂.

## Friendly Reminder

That's all for today's sharing. Here are a few important points to keep in mind:

1. Trancy and Glarity rely on the presence of captions in YouTube videos for one-click generation. Although you can use AI speech recognition like OpenAI Whisper, for now, you have to do it manually. Let's look forward to more convenient applications made by talented developers 😂
2. Glarity also has **Token limitations**, so it may not always generate complete content. It's recommended to select the content you need and generate accordingly. Alternatively, you can copy and paste the content into ChatGPT and ask multiple questions.
3. Glarity allows you to choose between GPT-4, GPT-3.5 Turbo, or OpenAI API for summarization. Their capabilities vary, with the most significant difference being generation speed. Feel free to experiment and find what works best for you.
4. The content generated by GPT series cannot guarantee complete accuracy. It's still necessary to **verify from multiple sources**. These tools are meant to help us accelerate knowledge circulation, but ultimately, professional explanations are essential.

## What do you think?

I hope you found this content helpful!

> If you'd like to see more tech news and applications, please subscribe to my free newsletter to stay up-to-date: <https://programmuren.substack.com>
>
> 1-2 newsletters per week, 3000 words, 6 minutes reading time - Explore tech journey with 300+ subscribers
>
> Your subscription and feedback are the greatest support for my writing 🥳
