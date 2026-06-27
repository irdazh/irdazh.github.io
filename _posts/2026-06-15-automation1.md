---
layout: post
title: AI Workflow Automation 1
categories:
- Automation
tags:
- backend
- pandas
- automation
description: Local python scripts for KPI reports automation.
media_subpath: "/assets/img/pandas"
date: 2026-06-15 00:00 +0000
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

Uhm, I started this projects a few weeks ago. Then, something came up abruptly, punched me in the face, and I ended up losing track of time... 

Those things, I made those up, kinda. However, oh well, if life is going to be a bit nicer to me in the future, the milestone I had in mind should look like this: 


1. Local python scripts for KPI reports automation.

2. Scripted integration with LLM APIs for research processing.

3. Image summarizer using LLM API thingies + hosted in Hugging Face space.

4. And at last, workflow configurations for zero code background execution using n8n pipeline. 

I've worked on some of those projects. And here, I intended to talk about the first one. 


In case wanna take a look at the repo, just go to: [https://github.com/irdazh/simple-pandas](https://github.com/irdazh/simple-pandas)!

## Approach

But you guys know what? It is way too simple, what should I even talk about? I just created automation for KPI reporting using python. That's it. 

The approach looks like this (and yes, I pasted them from the repo): 

1. Generate a dummy dataset: running a python script
2. Create automation.py python script
3. Run the script!
4. Report generated, consists of
   1. Total revenue
   2. Average revenue per category
   3. Items missing KPI targets

Take a look at this screenshot, and that's the end of it. No explanation needed. Bye!

![result](/result.png)_Reporting result_


