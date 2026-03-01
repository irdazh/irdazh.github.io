---
layout: post
title: Retail Sales Dashboard

categories: [DA Projects]
tags: [dashboard, business intelligence, retail sales]
description: "BI project: a simple dashboard on Retail Sales...." 
media_subpath: /assets/img/retail-sales-dashboard
---

# Context 
Uhm. It's mostly ChatGPT-ied -- so no wonder if it sounds soulless. Anw, have a nice day, as always.

A mid-sized retail company operates across multiple regions and product categories. While revenue looks good, management (?) observes fluctuations in profit performance and suspects that **discounting strategies** and **category-level inefficiencies** may be affecting **margin stability**.

Therefore, the company needs a structured analytical view to: 
- Identify sustainable growth drivers
- Detect margin leakage
- Evaluate discount impact across regions
- Optimize product portfolio performance

# Problem
Although sales performance appears strong, revenue growth does not consistently translate into profit growth. Profitability varies significantly across regions and product categories, suggesting uneven pricing discipline and structural margin inefficiencies.

Management lacks a consolidated dashboard that connects revenue, discounting behavior, and profitability performance to support strategic decision-making.

# Objective
So, let's design an interactive Business Intelligence dashboard, that: 
- Monitors overall business health
- Identifies high-performing and underperforming segments
- Highlights margin risk categories
- Provides actionable insights for pricing and portfolio strategy

# Tech Stack
- Tableau Public
- Public Superstore Dataset
- Power BI (indefinite, not yet tho, fufufu.)

# Dashboard Structure
## DB 1 -- Executive Summary
Provides high-level business health monitoring through: 
- Total Sales
- Total Profit
- Profit Margin %
- Total Quantity
- Average Discount
- Monthly Sales & Profit Trend
- Revenue & Profit by Region
- Top 10 Products Sub-category by Profit

Its main purpose is to give management a 10-second snapshot of performance and detect anomalies in trend or regional performance. 

## DB 2 -- Product & Profitability Analysis
Provides deeper analytical insights through: 
- Sub-category Sales vs Profit Quadrant Analysis
- Top Revenue Products
- Bottom Profit (Loss-Making) Products
- Subcategory-level performance clustering

Its main function is to identify growth drivers, margin risks, hidden opportunities, and portfolio cleanup areas. 

# Key Insights
## 1. Revenue and Profit Are Not Perfectly Aligned
Although sales and profit are generally correlated, peak revenue does not always generate peak profit. The highest sales month (~118k) produced only ~10k profit, while a lower sales month (~97k) generated the highest profit (~18k).

![trend](/trend.png)

This suggests margin compression during high-revenue periods, likely driven by heavier discounting.

## 2. Regional Performance Imbalance
- The West region generates the highest revenue and maintains the lowest average discount (~10%), resulting in strong profitability.
- The Central region, despite higher sales than the South, produces lower profit due to significantly higher discounting (~24%).

![region](/region.png)

In short, discount strategy strongly influences regional profitability. 

## 3. Technology as Growth Engine
![topright](/quadrant.png)
The Technology category consistently falls into the high-sales, high-profit quadrant. Products such as Copiers and Phones are major contributors to both revenue and profit.

![categories](/categories.png)

Technology is the company’s primary profit engine.

## 4. Margin Risk Categories
Furniture and certain Machine-related subcategories generate high revenue but relatively weak profitability.

![bottomleft](/quadrant.png)

This suggests structural margin inefficiencies that require pricing, discount policy, or cost review.

## 5. Hidden Opportunities
Subcategories such as Appliances and Paper demonstrate strong profitability relative to their sales volume.

![topright](/quadrant.png)
These segments represent scalable growth opportunities through targeted promotion.

## 6. Portfolio Cleanup Candidates
Several subcategories (Furnishings, Bookcases, and another 5 from Office Supllies category) contribute low sales and low profit, increasing operational complexity without meaningful financial contribution.

![bottomleft](/quadrant.png)

Rationalizing these SKUs may improve overall efficiency. Be wise tho, since it's not a one-size-fits-all solution -- lots of considerations are needed here. 

# 7. Recommendation
The primary management action should focus on: 
> Strengthening margin control by reassessing discount policies in underperforming regions and low-profit categories, while strategically investing in high-margin growth drivers such as Technology.

Specifically: 
- Review discount depth in the Central region
- Reevaluate pricing strategy in Furniture category
- Promote scalable high-margin segments (Technology, Appliances)
- Consider SKU rationalization for low-performing subcategories

# 8. Business Impact
This dashboard might help management to: 
- Align revenue growth with sustainable profitability
- Detect margin leakage early
- Make pricing and portfolio decisions based on structured data
- Shift from reactive reporting to proactive strategic planning

# Dashboard Preview
[Follow this link to play a live demo!](https://public.tableau.com/app/profile/daud.muhamad.azhari/viz/RetailSalesIntelligenceDashboard)

![db1](/db1.png)
_Preview of the 1st dashboard: Executive Overview_

![db2](/db2.png)
_Preview of the 2nd dashboard: Product & Profitability Analysis_

