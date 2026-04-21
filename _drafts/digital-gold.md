# MP01: Digital Gold Performance Dashboard

A mini project based on a job skill assessment test. 

I stumbled upon a skill assessment test for a job that I applied at some day in April. 
Since i thought it'll be a waste to just wing it once and left it to mold over time, 
I will just post it here, and rebrand it as a project. A crude, unrefined analysis.

Ah, I used a simulated dataset for this project. 
  
## Business Context

A specific company (Specom) launched a Digital Gold product that allows users to buy and sell gold digitally.
The business earns revenue from transaction fees.
This dashboard aims to:
1. monitor product performance
2. user activity, and
3. revenue growth to support business decision-making.

## Business Questions

- Is the product growing in terms of transactions and users?
- How much revenue is generated over time?
- Are users actively engaging with the platform?
- What is the behavior between buying and selling gold?

## Dataset

Synthetic dataset simulating 6 months of transactions (Jan–Jun 2024) that consist of:
- ~8,000 transactions  
- ~900 users  

Key features:
- Increasing transaction trend (product adoption)
- Gold price fluctuation with upward trend
- Buy-dominant behavior (early-stage product)

## Tools Used

- Tableau (dashboard & visualization)
- Python (data generation)

## Dashboard Preview

Add image here tho not yet. I haven't okay. 

![Dashboard Overview](images/dashboard.png)

## Key Metrics

- Total Transactions: ~8,000
- Total Revenue: ~70M IDR
- Total Users: ~900
- Avg Transaction Value: ~2.4M IDR

## Key Insights

### 1. Product Growth

Transactions increased significantly from ~100 to ~500 per week in 6 months, 
indicating strong product adoption.
Revenue followed a similar upward trend, suggesting healthy monetization.

### 2. User Engagement

Active users grew from ~100 to ~300 weekly in 6 months, showing increasing engagement alongside user base growth.

### 3. Buy vs Sell Behavior

Buy transactions dominate the platform (~14B vs ~6B total value), 
indicating users are primarily accumulating gold rather than trading.
It's a common thing in the early stage of a product (?) 

### 4. Revenue Dynamics

Revenue growth is strongly correlated with transaction volume, 
confirming the fee-based business model is functioning effectively.

## Business Recommendations

### 1. Encourage Sell Activity

Since buy activity dominates, introducing incentives for selling (e.g., lower fees or promotions) 
could increase transaction frequency and revenue.

But why should we focus on selling? Is it because it's the nondominated part? 

### 2. Improve User Retention

Although active users are growing, tracking repeat behavior and retention strategies (e.g., reminders, alerts) can further increase engagement.
Well, actually user retention is good enough. At least theoretically based on the initial simulation constraint.

<!-- ### 3. Optimize Mobile Experience
Given most transactions occur on mobile, improving mobile UX could significantly impact growth.
-->

## Limitations

- Dataset is synthetic
- No real customer segmentation
- No external factors (market events, promotions)

## 10. Future Improvements

- Cohort analysis (user retention)
- Segmentation (high-value vs low-value users)
- Profitability analysis per user group

<!-- 
## 🟩 ADD 1: Engagement Rate (VERY STRONG)

You already have:

* total users
* active users

👉 Add:

```text
Engagement Rate = Active Users / Total Users
```

---

👉 Insight example:

```text
Engagement rate increased over time, indicating not only user growth but improved platform stickiness.
```

---

---

## 🟨 ADD 2: Buy vs Sell Ratio Over Time

Right now you only have totals.

👉 Add trend:

* weekly buy vs sell

---

👉 Insight:

```text
Buy dominance persists over time, suggesting users treat the product as long-term investment rather than trading.
```

---

---

## 🟦 OPTIONAL (ONLY IF YOU WANT EXTRA EDGE)

### Monthly deep dive

Pick 1 month:

* April for example

Answer:

* peak activity?
* anomalies?

👉 but honestly:

> Not required unless you want extra polish

--> 
