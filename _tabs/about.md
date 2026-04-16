---
# the default layout is 'page'
icon: fas fa-info-circle
order: 4
---

<!-- > Add Markdown syntax content to file `_tabs/about.md`{: .filepath } and it will show up on this page.
{: .prompt-tip } -->


Hello, *Kawan*!

I am Daud, a soon-to-be well-versed Data Analyst (Scientist) with a drizzle of ML capabilities. 
Currently, I am learning things I knew well and beyond, as I always intend to do. 
Lemme boast about (not) all of my projects I've done during and post university time.

Oh btw, I did join and won lots of competition.
Bad news, I didn't make a decent documentation about them (Ah, all the more university projects).
But then, check these 
[repo](https://github.com/irdazh/Competitions) and
[awards](https://irdazh.github.io/posts/awards/)!
And in case of getting curious, check
[these certifications](https://irdazh.github.io/posts/certifications/)
as well!

Here we go.

## [Corn Leaf Disease Detector](https://irdazh.github.io/posts/leaf-disease/)

 Can we detect corn leaf disease and automate it using computer vision?
 (Ah, of course, it's conceptual only. I won't deal with the hardware thingamajig.)

   ![CLDD](/assets/img/leaf-disease/demo1.png)_Corn leaf disease detector deployed using streamlit app_

 Using corn/maize leaf disease dataset I found in kaggle,
 I trained simple and complex CNN model (and fine-tuned pre-trained complex models such as ResNet and MobileNet).
 I then deployed them online via Streamlit!
 (For local deployment I use FastAPI backend + Streamlit frontend:
 oh don't ask me how to do this and that, I just vibe-coded them~) 

 The model performs well with high accuracy (89%), although a bit low on some metrics due to a slight imbalance.
 And, uhm, uh, yeah, you see... it's slightly overfitting, which is perfectly normal!  

 Yeah, pretty sure that's that, and check these out: 
 [repo](https://github.com/irdazh/leaf-disease/),
 [article](https://irdazh.github.io/posts/leaf-disease/), and
 [demo that actually works!](https://leaf-disease-deploy.streamlit.app/) 
 
## [Churn Analysis](https://irdazh.github.io/posts/churn-analysis-sql/)

   ![CA](/assets/img/churn-analysis-sql/monthly_density.png)_Higher monthly charges correlate with higher churn rate_

 Why do you think customers churn?

 I analyzed a telecom dataset using SQL and Python and found:
 (1) short tenure customers churn the most,
 (2) month-to-month contracts drive churn, and
 (3) high charges correlate with churn

 Check these out:
 [repo](https://github.com/irdazh/churn-analysis-sql) and
 [article!](https://irdazh.github.io/posts/churn-analysis-sql/)


## [Customer Review Sentiment Analysis](https://irdazh.github.io/posts/customer-review/)

   ![CR](/assets/img/customer-review/dashboard.png)_Customer review dashboard overview_
 
 Are customers actually satisfied, and if not, why?

 I analyzed an e-commerce reviews dataset, did a sentiment analysis by using classifier models,
 went unsupervise learning using LDA to do a topic modeling, and host those models online via Streamlit.

 Although it failed (online). Haha.
 
 Well, something went wrong on the pipeline thing, so it won't run online. For now, let's just call it a day. 
 And check these out:
 [repo](https://github.com/irdazh/customer-review/),
 [article](https://irdazh.github.io/posts/customer-review/), and
 [the failed demo!](https://customer-review.streamlit.app/)

## [Inventory Analytics Dashboard](https://irdazh.github.io/posts/inventory-analytics-dashboard/)

   ![IAD](/assets/img/inventory-analytics/overview.png)_Inventory health overview dashboard using Tableau_

 Stock efficiency, supplier risk, and the optimization in between!

 Yes, it's another trivial Tableau dashboards, so what?
 Consists of inventory health overview and inventory efficiency analysis.

 Uhm, anyway, just check these out:
 [article](https://irdazh.github.io/posts/inventory-analytics-dashboard/) and
 [demo!](https://public.tableau.com/app/profile/daud.muhamad.azhari/viz/InventorySupplyChainAnalytics/Dashboard1)
 
## [House Price Prediction](https://irdazh.github.io/posts/house-price-prediction/)
  
   ![HPP](/assets/img/house-price/hpp-app.png)_House price predictor deployed using streamlit app_
 
 How much money should you spend for a decent (fictional) house?
 I analyzed a house price dataset, made an ML model using XGBoost in Python, and deployed them via Streamlit.
 Yes, another boring template project from an endless stream of tutorial trap. Eh?
 
 Check these out:
 [repo](https://github.com/irdazh/house-price-prediction/),
 [article](https://irdazh.github.io/posts/house-price-prediction/), and
 [demo!](https://irdazh-house-price-prediction.streamlit.app/)

## [Retail Sales Dashboard](https://irdazh.github.io/posts/retail-sales-dashboard/)

   ![RSD](/assets/img/retail-sales-dashboard/db1.png)_Executive overview dashboard using Tableau_

 A quick question, why doesn't revenue growth consistently translate into profit growth?
 The answer are: pricing (or discount) strategy, (structural) margin inefficiencies, and what else?

 Using a dummy sales dataset, I made two Tableau dashboards, one contains executive summary
 while the other contains a simple analysis on product & profitability, and then found:
 (1) revenue and profit unalignment, (2) regional performance imbalance,
 (3) technology category as a growth engine, and (4) some margin risk categories to evaluate.

 Check these out:
 [article](https://irdazh.github.io/posts/retail-sales-dashboard/) and
 [demo!](https://public.tableau.com/views/RetailSalesIntelligenceDashboard/ExecutiveOverview?)

## [Drug Consumption Prediction](https://irdazh.github.io/posts/drug-consumption-prediction/) 
 
   ![DCP](/assets/img/drug-consumption/nemenyi-f.png)_Nemenyi test for comparing models & methods performance based on F1-score_

 Ah, tbh, I have got enough of this imbalance dataset combined with threshold optimization.
 It's a (useless and trivial) undergraduate thesis. Oh gosh, \**goosebumps*.

 Yes, I actually analyzed that kind of trivial thing. But nope, no need to check this out:
 [repo](https://github.com/irdazh/final-project) and
 [article!](https://irdazh.github.io/posts/drug-consumption-prediction/) 




<!-- I am Daud, currently unemployed with one short job experience. A (kinda) fresh graduate in Statistics from Universitas Gadjah Mada. It's supposed to be a place where I **pridely** put all my portfolios. Will it come in handy, someday, in the future, though?

Nope. Probably not.

And guess what? I played this game wrong! So, let's replan for a bit: separating the readme and github pages. Right, should be plausible at this rate. Yak, semangat bang. 


## Just whine for a bit
I always think that I'm pretty skillful in lots of data-related tasks. Although in reality, I'm just another mediocre in this field. I'd love working with data: getting some contexts out of their abstractness, building a useless utterly-complex machine learning model just for fun, copy-pasting lines of codes into some projects, and anything else in between. 

It's another boring afternoon. Sitting on a chair, in a damp stuffy bedroom. Overthinking everything, keep replanning things, without any actual execution. Like seriously, what else could I do, dude? 

*Sigh*. I always believe that things will eventually get better, since that what life is all about. One even said that we just had to keep learning, and pushing in any kind of situation.

So here I am. Wasting my time typing all this nonsense. Trying to stay sane despite all the boredom creeping inside the body. -->
