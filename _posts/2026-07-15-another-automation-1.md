---
layout: post
title: Another Automation 1
categories:
- Automation
tags:
- automation
- Python
- Colab
description: 
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

I didn't make any GitHub repo. At least not in my own, personal repository. Shall we talk about how things have been recently? I got my second job. It's in the business and economical thingies (?) in Indonesia. As you might guess it: Jakarta!

The company isn't well known. The salary? Oh well, it's much lower than I expected, but now, I even questioning my competencies and capabilites, LOL. Am I that bad?

Therefore, I don't bring it up to friends I had in college. Not that many people know I'm here. Geez, I can't brag this thing up, okay? So that's why, I'm staying under radar right now. To be honest, I wanna meet them. Hearing them talking about whatever that is. However, on the other side, I can't show myself up just yet. I hate to say this, but I envy them, I can't deny this feeling. It's so overwhelming. I'm indeed pitiful, but at the same time, I don't want them to pity me. 

Ego, that's it. 

*Wait, isn't it supposed to be a blog where I put my projects and portfolios? What the what am I blabbering about right now?*

***

## Problem

Anyway, enough for now. As for the first few weeks in this new job, honestly, it's fun. I'm handling automation project for quality assurance of operational staffs (here, we will call it advisor). In simple term, I'm trying to automate how QA team assess the advisors' quality by analyzing their conversation via chat with the client (?)

In total, there are 6 dimensions to be evaluated. For now, we will focus on the first dimension: responsiveness and availability. When it's inside the advisor working hour, they are supposed to be responsive and available at any moment to answer any chat from the customer. ASAP.

## Approach
From here, I could've just implement the rubric made by QA team. They evaluated the advisor's responsiveness by assigning score 1 till 4 depends on how much time for them to response to the customer in their working hour. Sounds simple, right? 

Good grace, when I joined this company, someone has already started working on this project. A blueprint. I got a rough, dented one. Oh, don't get me wrong, I actually felt really grateful for it. There were lots of things to be revised, but at least, I didn't have to do it from scratch.

The legacy code, let's put it that way, was decent enough. It could read raw texts with various formats, parse them into unified format, which consists of timestamp, sender, and also the texts themselves.

After it generated such table, it identified which one is the advisor which one is the client. Then, for each client's chat, it measured the advisor's response time. There are several exceptions: when the client texts outside working hour, when the client's chat is a closing message (such as 'thanks' or 'okay'), and i think that's all (?)

Well, after it got the measured response time, it then converted it into point ranged from 1 until 4, then averaged those all values into one representative score for each advisor. 

I made some adjustments, through several iterations.

1. Starting with the file reader. Instead of doing it one by one, I decided to do it in one go, using zipped file that contains all of the advisor chat. I'm thinking of reading directly from google drive, but for now, it will do. 

2. The legacy code's of deciding the advisor between the two senders were using the keywords advisor used as accounts name. Well, unfortunately, the naming standard is inconsistent (some even have 'You' as the name, which I think depends on how they download the chats). So, for each advisor, I'll just assign the sender with the most frequent existence as the advisor's account. Uhm, it still is a problem when the advisor have several accounts tho. Oh, gosh. 

3. There were some files failed to extract. I analyzed them, and found out that they had different timestamp format so the parser couldn't parse them in the desired format. I added those kind of timestamp format. 

4. I also add another exception: shifting the client's chat time when it's a break time to working time (e.g.: from 12.00 until 13.00 shifted to 13.00).

5. As for representative score for each advisor, I strictly followed the QA team manual method, find the worst representative score for each clients. Then, I write those output to the sheet.

I think that explains the general idea about how this automation thing work.

## Key Findings

Compared with manual assessment QA, there are definitely some error. Uhm, I actually did it with number, but to be honest, the evaluation metric used isn't a proper one. I did not compare per one client, but instead, comparing the advisor's average score. 

It wasn't accurate, of course, but in my opinion, it at least gave a rough idea how both of the method compared. Well, I chose it out of convenience, I didn't have the time to label each samples (be it manual or automation) with the respected client's name. Yup, I was and still am, lazy. 

As for the more substantial error, there are several cases from manual QA that I couldn't be included in the automatioon logic. First, we can't include when one still activate the automated message during the working date. There's just no data to determine the advisor's working date. Second, there are several cases that I personally didn't agree on how the QA team giving the score for them, but oh well, not that I can argue with them. Lastly, there were some cases where the timestamp just got messed up, and of course any evaluation made using automation will be straight up invalid. 

## Deployment

Oh my, should I include this part as well? 

Deployment? Uhm, I'm working in colab for this project, then directly write the result onto the google sheet. So uhm, I combined google colab, google drive (on going progress), and also google sheet for this one project....

Will the above lines do? *I guess.*

## Personal Vendetta
 
I love working with this project. Thanks for mas parter, whom I should report to, for filtering and handing me the right project. I made a huge modification through several iterations, discussed a bit with QA team, and now (uhm, around one month after this back-date post-date), I'm finishing thing up.

Until next time, I guess. *Oh gosh, I still have to write another 4 posts.*