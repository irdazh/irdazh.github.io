---
layout: post
title: Spreadsheet Automation
categories:
- Automation
tags:
- Automation
- Python
- Spreadsheet
description: Part of automation project for staff QA.
media_subpath: "/assets/img/automation"
date: 2026-08-15 00:00 +0000
---
<!-- 

Parts
1. What you did + screenshot + follow these links
2. the problem -> approach -> key findings -> deployment -> what i learnt: conclusion -> demo  
3. Put lots of images. I guess. 

LinkedIn

-->

## Chatter

Based on the contract, it's my last month in this company. The company and I haven't talked about contract renewal. Well, truths be told, I'm not really in the mood of discussing that thing, since I overheard one talking about not being able to increase its salary.  

So, I guess, I have to execute the exit plan, now? Haha.

Anyway, enough for now. Uh, remember the way I was milking the staff QA project? I'll add another layer here, since the objective is to post anything, regardless the quality.

Yeah, since no one really read this blog (?) to begin with. And even if one ask AI to summarize this portfolio site, what do I care? LOL. 

***

## Problem
For the staff QA project I previously discussed, although I called it automation, it doesn't work 100% automatically. It still needs human touch to actually run the code. 

Since I put the code in Google Colab, I still have to run the code manually once per week. There are also some parts that need a constant editing due to some data inconsistencies (and also my incapabilites). So, forcing it to work 100% automatically is out of question. 

Once we got the result, actually, I gotta try doing a new automation approach for transforming the result. 

There was problem when there were two sources of result: first one was from the manual QA, and second one was from the new automation QA. They had different format, one was in wide format, and the other was in long format. Meanwhile, we had to combine those two result, since there was a request from the other team. What a headache.

## Approach

I first tried transforming inside the spreadsheet. But the formula? I found it super hard to understand it, LOL. it was way to compilated for me. And even with the help of LLM, I still found it complicated and I guess it was also prone to error (?) Not sure anymore, tho. 

Therefore, I used Python. I just had to (ask an LLM to) write a simple reading, transformation, and merging to clean and combine those two source of results. There were definitely lots of error (and revisions), but I was pretty content with the idea itself. 

Well, I did use colab for creating a pilot project, where I could draft and experiment with the code before making the automation. As for the automation, after discussing with LLM, we could utilize GitHub Actions to run the code for us as scheduled.

Although the setting was pretty confusing at first, but of course, I could handle it just well. 

## Deployment
Was it deployed?

As I stated earlier, the automation itself was run using GitHub Actions. It read the data from several sources (although now, it only reads from one source), cleaned, transformed, and merged the data, before writing them into a single, compiled result.

## Personal Vendetta
 
There are several other projects where I also used this kind of approach for the automation part. Especially, when I have to deal with updating data based on a time trigger.

Now, thinking about it again, my approach is kinda dumb in a way. There are lots of steps where I probably could utilize a state-of-the-art LLM in a more efficient way -- but for now, that kind of approach was way confusing for me.

Yeah, I still view an LLM as a single, kinda pro, assistant. I haven't changed the way I worked with it, which is by now, is kinda concerning. Anyway, the anxiety sure is for later.

With that in mind. I have found a dumb way when debugging the code, especially when we aren't that pro: do trial and error in colab and use the clean, refactored code in the GitHub python file. 
1. Depends on the error, we might be able to solve it directly in the GitHub, without having to actually break the code apart. Especially when it's related with api connection error or missing library, or some obvious error. 
2. As for a more complicated error, we might have to copy the code back to the colab. 
3. Modify the auth & configuration part: since they might differ a lot between Colab and GitHub environment. 
4. Make sure to disable any writing/updating database part. 
5. Find the error. Isolate and examine the error part.
6. Since the original structure might be inside a function, I think, for running code in Colab, it's better to break the function apart, and running them line by line, while observing the part result in error. 
7. Once it solved, update the GH code, and also make a comment, both in commit and in the colab. 
8. That's it.

Ba iii.