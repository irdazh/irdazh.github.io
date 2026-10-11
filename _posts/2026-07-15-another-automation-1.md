---
layout: post
title: Another Automation 1
categories:
- Automation
tags:
- automation
- Python
- Colab
description: Automation project for staff QA. 
media_subpath: "/assets/img/automation"
date: 2026-07-15 00:00 +0000
---
<!-- 

Parts
1. What you did + screenshot + follow these links
2. the problem -> approach -> key findings -> deployment -> what i learnt: conclusion -> demo  
3. Put lots of images. I guess. 

LinkedIn

-->

## Chatter

I didn't make any GitHub repo. At least not in my own, personal repository. Shall we talk about how things have been recently? I got my second job. It's in the business and economical (?) area in Indonesia. As you might guess it: Jakarta!

*Blabber-blabber*.

Ego, that's it. 

*Wait, isn't it supposed to be a blog where I put my projects and portfolios? What the what am I blabbering about right now?*

***

## Problem

Since it might contain some of company's secrets, let's make things more secure (?)

**Introduction thingies...*.

**With the objective be evaluating chat responsiveness*.

## Approach
From here, I could've just implement the rubric made by QA team. They evaluated the advisor's responsiveness by assigning score 1 till 4 depends on how much time for them to response to the customer in their working hour. Sounds simple, right? 

Good grace, when I joined this company, someone has already started working on this project. A blueprint. I got a rough, dented one. Oh, don't get me wrong, I actually felt really grateful for it. There were lots of things to be revised, but at least, I didn't have to do it from scratch.

The legacy code, let's put it that way, was decent enough. It could read raw texts with various formats, parse them into unified format, which consists of timestamp, sender, and also the texts themselves.

**Some useless details was over here*.

I made some adjustments, through several iterations. I explained in detail in 5 points. 

I think that explains the general idea about how this automation thing work.

## Key Findings

Compared with manual assessment QA, there are definitely some error. Uhm, I actually did it with number, but to be honest, the evaluation metric used isn't a proper one. I did not compare per one client, but instead, comparing the advisor's average score. 

It wasn't accurate, of course, but in my opinion, it at least gave a rough idea how both of the method compared. Well, I chose it out of convenience, I didn't have the time to label each samples (be it manual or automation) with the respected client's name. Yup, I was and still am, lazy. 

As for the more substantial error, there are several cases from manual QA that I couldn't be included in the automatioon logic. First, we can't include when one still activate the automated message during the working date. There's just no data to determine the advisor's working date. Second, there are several cases that I personally didn't agree on how the QA team giving the score for them, but oh well, not that I can argue with them. Lastly, there were some cases where the timestamp just got messed up, and of course any evaluation made using automation will be straight up invalid.

Oh, I could actually ignore some, if not, most of them by using keywords we could found in the automated message. It's messy and lots of exceptions, but what can we do? 

## Deployment
Oh my, should I include this part as well? 

Deployment? Uhm, I'm working in colab for this project, then directly write the result onto the google sheet. So uhm, I combined google colab, google drive (on going progress), and also google sheet for this one project....

Will the above lines do? *I guess.*

## Personal Vendetta
 
I love working with this project. Thanks for mas parter, whom I should report to, for filtering and handing me the right project. I made a huge modification through several iterations, discussed a bit with QA team, and now (uhm, around one month after this back-date post-date), I'm finishing thing up.

Until next time, I guess. *Oh gosh, I still have to write another 4 posts.*