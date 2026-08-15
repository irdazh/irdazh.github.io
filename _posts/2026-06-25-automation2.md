---
layout: post
title: AI Workflow Automation 2
categories:
- Automation
tags:
- backend
- automation
- AI
- Gemini
description: Feed a research paper to AI, and let it digest it? Wha, what a moron.  
media_subpath: "/assets/img/research"
date: 2026-06-25 00:00 +0000
---
<!-- 

Parts
1. What you did + screenshot + follow these links
2. the problem -> approach -> key findings -> deployment -> what i learnt: conclusion -> demo  
3. Put lots of images. I guess. 

LinkedIn

Since it's getting out of hand, I tried implementing (?) an LLM model as a chatbot. I just called their API and put it into a (not so) good use...

I put the model in a photography chatbot, and found: nothing! 

B-but I learnt a (few) lot:
- Creating a FastAPI backend part
- A Streamlit frontend 
- Dockerfile containerization
- And a nice deployment using Hugging Face space
- Well, the potential is HUGE. 

Check them out: 
 - https://irdazh.github.io/posts/chatbot-ai/
 - https://irdazh-chatbot-ai.hf.space

-->

## Chatter

Shall I just copy paste things from the GitHub repo? I don't feel like telling any lies this time. 

Yeah, it's the second step towards automation thingy. After using such simple (and kinda useless) pandas in python, it's time we finally utilize the AI for whatever reason there is. 

So, it's supposed to be a great help for anyone wondering what does a research paper really talk about? I mean, I, a commonner, find it hard to read a research paper, let alone understanding them and make a valid conclusion. 

There you go, just upload it to the AI, and process it in (less than) a minute! Ta da!

In case wanna take a look at the repo, just go to: [https://github.com/irdazh/research-assistant](https://github.com/irdazh/research-assistant)!

## Approach

Yeah, just put several lines inside a function so that it could call the Gemini's API, upload the file there-I-don't-know-where, let the AI analyzing it based on the data (and prompt, and output schema we defined), and viola, we got the result!

![result](/result.png)_Summarization result_

Yeah, but you'll find it hard trying them yourself. Good luck in that case!
