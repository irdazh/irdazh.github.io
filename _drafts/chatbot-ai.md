---
layout: post
title: Photography Chatbot AI
categories:
- DS Projects
- BE Projects
tags:
- backend
- streamlit
- chatbot
- ai
description: Experiment on making an AI Chatbot using FastAPI combined with Groq service
  and deployed via Hugging Face space.
media_subpath: "/assets/img/chatbot"
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

Guess what? Once upon a time, I found an internship position for AI Engineer role. I of course got excited about it, thinking it might be related to ML Engineer as well as Data Scientist.

I was wrong. Upon looking things up via Google and LLMs, I found out AI (and ML) Engineer is a role that mostly dealing with model deployment. They build the infrastructure to host the AI/ML model inside the app, via cloud, or just calling the API (?). Well, in my shallow underestanding, it might highly similar with backend position rather than DA/DS position. 

Therefore I started learning these sort of things. Focus on deployment, putting AI model in use, making a simple backend infrastructure, as well calling the API....

Which, to be honest, it made little to no sense for me till now. And this page is part of this whole lesson.

<center> *** </center>

**Enough with the chatter**. So, in this project, I ended up building a Photography Chatbot AI. 


![preview](/preview.png)_Preview of the online app (?)_

I utilized FastAPI (as what? idk what to call it), combined with Groq AI Service as the brain, then connected it to the frontend Streamlit UI. At last,
for online deployment, I hosted it via Hugging Face space.

Well, do follow these links: 
* Live demo: [https://irdazh-chatbot-ai.hf.space](https://irdazh-chatbot-ai.hf.space)
* GitHub repo: [https://github.com/irdazh/chatbot-ai-tutorial](https://github.com/irdazh/chatbot-ai-tutorial)


## Approach

Since I'm (not that) lazy, I copied-pasted several things from the README file...

As I explained earlier. I did create a backend Groq brain with Llama model. 

*Wait, what's the use of FastAPI here? Ah, beside defines input and output model/type, it also creates an endpoint -- the address where we did preprocessing and called foreign AI model*

That clears 60 percent of your understanding gap.

Next, I connected the backend part with frontend Streamlit UI. It looked so simple. Well, I then deployed them offline and online, using UGH, alien command texts directly or by creating the Dockerfile first. 

For the online deployment, you've already known it, I hosted it via Hugging Face space. *Should I highlighted all these tools stack I mentioned LOL.*


## Key Findings

Nah. I don't think I found anything. But it was pretty fun LOL.

## What I Learnt

A whole LOT!
1. FastAPI backend part
   1. Secret credentials in `.env`
   2. Pydantic basemodel for input
   3. A post API endpoint, where we do preprocess and call a foreign AI model 
   4. Raise HTTP Exception error
   5. Add a simple memory for the convo
2. Groq AI model
   1. LLama 70b versatile
   2. With 0.7 temperature
3. Streamlit frontend part
   1. Trivials: page config, title, icon, session state
   3. Get input from the user
   4. Request post point to backend to get a response
   5. Display the chat
4. Dockerfile 
   1. Tho still lots of holes here and there, I think I learnt a lot about containerization
   2. It worked well in offline, other's env, even online in HF space!
5. Next, I will explore a bit more about handling system for AI/ML models. Or even, I'll go to do some automation using state-of-the-art framework! Who knows...


## Demo
Well, I tried embed the space here. Since it works offline, does it also work online? 
Else [click this!](https://irdazh-chatbot-ai.hf.space)


<iframe
	src="https://irdazh-chatbot-ai.hf.space"
	frameborder="0"
	width="850"
	height="450"
></iframe>



