---
layout: post
title: Another Automation 2
categories:
- Automation
tags:
- automation
- AI
description: AI automation project for staff QA, part 2.
media_subpath: "/assets/img/automation"
date: 2026-07-25 00:00 +0000
---
<!-- 

Parts
1. What you did + screenshot + follow these links
2. the problem -> approach -> key findings -> deployment -> what i learnt: conclusion -> demo  
3. Put lots of images. I guess. 

LinkedIn

-->

## Chatter

Well, I overshared my current life in the previous post, no? Idem with the previous post, I also wrote this post in the future, technically speaking. 
***

## Problem

The detail of the problem could be read from the previous post. There are several dimensions we use to assess the advisors quality. As we have discussed the first dimension, now, it's time to discuss the next 3 dimensions: communication clarity, personalization, and tone & empathy. 

As you can guess it, we're moving into NLP realm: where everything is dirty and ambiguous. We could, of course, train our own model. However, considering the problems complexity, where we must asses the informal conversation between the advisor and the client, training our own model is just an impossible thing to do. Don't you agree? 

Just to train our own model, we must preprocess our data: from cleaning without removing its contextual meaning and nuances, transforming them into numerical values model could digest, finding the correct problem-solution set, and the list just goes on. 

To make things even worse, for those three dimensions, we must include both the advisor and the client conversation, but only assessing the advisor performance. In our limited understanding, training our own model to be able to understand that kind of context, is impossible.

So we resort on utilizing AI to do the complicated work: complex text classification.   

## Approach

Ah, since I'm getting lazier each day, I'll just delete the contents from this point on. You could always read the original passage tho. Just turn back the time, technically, I know, you can. 

Actually another update from the future: I now have 3 colab I have to run once a week (or more). Ah, I'm keeping this line below, it just sounds so me. 

_For future me, I strongly urge you to make a rough structure before writing anything. So that we don't have to_ muter-muter _like this!_

Tools I utilized here:
1. Python in a Colab
2. Drive and sheets connection: to read the files and write the result
3. AI API thingamajig: that's that, don't ask me the details



