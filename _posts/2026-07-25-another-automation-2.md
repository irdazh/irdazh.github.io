---
layout: post
title: Another Automation 2
categories:
- Automation
tags:
- automation
- AI
description: AI automation project for staff QA. 
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

We parsed the conversation file into table readable to human -- which we've built for the previous problem! We then preprocessed the data, added several guardrails along the way, including file removal for a short conversation. We then change the format into one AI could easily read. Call the AI via API (uhm, to be honest, I don't even know what's the correct phrase/wording), then save the result!

That's it. Easy, right? 

Oh, ups, not that straightforward. 

Apparently, I did lots of trials and errors. Since I'm not that fluent on using AI, I needed to tweak lots of things, here and there. I experimented using several models: from GPT open source models, and also Gemini Flash (Lite) models.

Since they're a highly probabilistic model, expect some variance during prediction (re: classification). We adjusted the parameters handling the variability, but it couldn't remove the variability completely. Well, the variability wasn't that big to begin with (_*uhm, not all..._).

Anyway, we ended up using Deepseek model. What a plot twist, right? Of course, because it's much cheaper, and to be honest, another team has built and applied this kind of QA project. Although the approach was kind of different compared with ours.

_For future me, I strongly urge you to make a rough structure before writing anything. So that we don't have to_ muter-muter _like this!_

Tools I utilized here:
1. Python in a Colab
2. Drive and sheets connection: to read the files and write the result
3. AI API thingamajig: that's that, don't ask me the details

## Key Findings

Since the manual rubric was highly subjective (in my opinion), the error itself was pretty big. Well, truth be told, I didn't take it as the sole criteria before implementing the model. Even when the error was below the standard, I decided to implement it anyway. Uhm, not that the users understand it right, technically speaking? I could've just sugar coating it and let them choose their demise on their own.

Right? 

Thinking about it again, it might have been deployed prematurely. The AI has (slightly) different bias compared to human evaluators, but I implemented it anyway. Yeah, we human just weren't patient enough. It's not a bad decision, tho, because we still asked the human evaluator to take random sampling to assess the AI performance.

They (just) said that the result pretty accurate. Although, I myself, doubted it. 

## Deployment

Idem with previous project. Yeah, write the result directly to the target sheet. Although, I still have to run it manually....

## Personal Vendetta
 
I love working with this project. Thanks for mas parter, whom I should report to, for filtering and handing me the right project. I made a huge modification through several iterations, discussed a bit with QA team, and now (uhm, around one month after this back-date post-date), I'm finishing thing up.

Oh, there are actually two more dimensions. If the 4 previous dimensions measuring the overall conversation hygiene advisors must have, these 2 next dimensions measuring their sales skills. These two dimensions don't always exist for each conversation, making it harder to actually classify and also measure the error.

So, even I am not convinced enough with my own method. I just served it along with the other dimensions, came to the users face, and said: use it, or leave it, it's all up to you!

Nah, that definitely didn't happen. But, oh, well, they used as a prescreening, uhm, perhaps (?)

Until next time. *Oh gosh, I still have to write another 3 posts.*


