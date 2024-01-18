---
layout: default
title: Customer Marketing
parent: XRAI Examples
grand_parent: Guidelines
nav_order: 1
---

# Customer Marketing
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

Marketing is the business of crafting, promoting, and selling goods and services. It plays an important role in enabling and facilitating the relationship between producers and consumers. The practice of marketing is inherently not ethically neutral and can be harmful especially to potential customers or consumers. Some products may have a significant potential for causing harm to its consumers, such as fast food, alcoholic beverages, and tobacco. With this, even if a product is not inherently harmful, its promotion can be ethically dubious, as advertising can rely on the deliberate nudging and manipulation of people’s wants and desires. It should also be noted that even if a product is not intrinsically harmful nor its promotion manipulative, it may still lead to harm and distress for the customer. A good example is a customer being harmed by defaulting on a loan. 

It is thus essential to account for ethical considerations when assessing and designing marketing systems; this naturally includes the decisions being made with the help of AIDA/DSAI systems. Such examples include: 
- **Content generation** – generating personalized content for customers based on customer profiles 
- **Web and App personalization** – leveraging real-time and historical data to customize web and app pages displayed at different purchases stages as per their interests 
- **Targeted offers** – determining the likelihood of customers purchasing a product conditioned on receiving an incentive or marketing offer like a discount 
- **Channel assistance** – supporting customers in their purchases across different channels of communication 

## Input 
Depending on the use case, DSAI-influenced marketing systems usually use machine learning models to predict customer responses to marketing interventions. Usually, these systems have the following components: 
- **Population from which selection occurs** – may be existing customers or potential leads; regardless, there exists tabular information of individuals 
- **Defined set of marketing interventions** – depending on the use case, this denotes how the institution/company interacts with the customer (ex. Through email, having a customer representative, applying discounts) 
- **Objectives for selecting individuals** – depending on the use case, this could be propensity modelling for purchasing products, cross-selling or up-selling, customer attrition likelihood rates, or maximizing profits on customers who are already going to buy products 
- **Algorithmic implementation** – these may be automated business rules or ML algorithms to select these individuals or products to which selected individuals will like 
- **Matching records of marketing endeavors and sales outcomes** – allows institutions to calculate the effectivity of the marketing system 

Due to these factors, there should be stressed importance in describing the system objectives and context. We provide reflective questions to guide in your system design: 
- Who are the customers/leads from which the system selects individuals for marketing interventions? 
- What are the natures of the marketing interventions and how are they assigned? 
- If the DSAI system uses a rank to select customers, is it using a propensity-based or uplift modelling-based approach?  
- Is the intervention method the same for all customers, or are there sets of interventions that the system selects between? 
- Does the system apply eligibility rules for products or services being marketed? Or are defining these rules part of the system selection process? 
- Does the system have business rules or event triggers in addition to the predictive model(s) being made? How are these rules or triggers determined? 

DSAI System Owners should carefully analyze their systems with reference to their XRAI objectives and determine possible harms and benefits. Such examples include: 
- Benefits from receiving a marketing intervention 
    - Interventions that provide incentives or discounts may provide something of value to the customer, regardless of their subsequent actions 
    - Interventions that lessen lead times or show priority to the customer may be interpreted as valuable  
- Harms from receiving an unwanted marketing intervention 
    - Interventions that clutter or distract, such as unsolicited emails or text messages 
    - Calls or other forms of interventions for products/services not interesting to the customer may cause annoyance and backlash 
- Benefits from acquiring a product or service – Ideally, the product being marketed has a direct benefit to the consumer 
- Harms from a failed application 
    - Submitting an application costs time and effort wasted if the application outcome is negative. 
    - This is more relevant if the marketing intervention causes the customer to apply 
- Harms or benefits from a longer-term outcome 
    - Failed applications for certain products may also lead to more difficult application attempts in the future 
    - Accepted applications or successful acquisitions may be rewarding in the short-term, but if the customer is unable to continue pursuing the product requirements after success, it could lead to harmful outcomes ex. Defaulting on loans 

## M&O 
The choice of performance measures is dependent on the approach(es) used and entails consequences for the operation of the DSAI system. It is recommended that the following measure of performance would be analyzed during model development: 
- Empirical lift 
- Class balanced accuracy 
- Cross entropy loss 
- Area under the curve 
- Confusion matrices 

In the previous section, we showcased the need to identify potential harms and benefits of deploying the marketing DSAI system. Aside from typical technical performance measures, it is good practice to design quantitative metrics to measure or estimate the impact of harms and benefits. We can consider quantifying the incidence rates of typical harms and benefits of a marketing system as an example. 

Let S be a random variable that describes the likelihood of targets from the DSAI system, S ∈{0, 1}. Let A be a random variable denoting the personal attribute that is used to analyze the system’s XRAI principles, taking values  A ∈ {0, …, K}. Let us also reference possible outcomes with shorthands: Applied for product being App, the Acquired product as Acq, and Resolved product as Rvd. We can use these to present lift scores or probabilities that describe benefits or harms based on marketing interventions. Let us denote A = sex and a = woman. 
- **Benefit of receiving the intervention**: P(S = 1 \| A = a). Given an incidence rate of 0.2, we can say that “women are selected 20% of the time”. This is the same as the demographic parity fairness measure if compared across cohorts. 
- **Harm from receiving an unwanted intervention**: P(S = 1 \| App = 0, A = a). With an incidence rate of 0.3, we can say that “women that don’t apply for the product receive the intervention 30% of the time”. This is also known as the false positive (FP) rate. 
- **Benefit from acquiring the product**: Z(Acq = 0 \| App = 1, A = a) = Pd(Acq = 0 \| App = 1, A = a) − Pc(Acq = 0 \| App = 1, A = a). Here we define the additional number of women who acquired the product divided by the number of women in the cohort. Thus, with an impact rate of 0.1, we can say that “the system caused a 10% increase in the rate women acquire the product”. 
- **Harm from a failed application**: Z(Acq = 0 \| A = a) = Pd(Acq = 0 \| A = a) − Pc(Acq = 0 \| A = a). This shows the number of additional women that applied for the product and had their application rejected. Given an incidence rate of 0.1, we can say that “the system caused a 10% increase in the rate at which women had their applications rejected”. 
- **Harm from a long-term outcome**: Z(Rvd = 0 \| App = 1, A = a) = Pd(Rvd = 0 \| App = 1, A = a) − Pc(Rvd = 0 \| App = 1, A = a). This shows the number of additional women which acquired this product and did not pursue continued usage, divided by the number of women that acquired the loan. If the product is a credit card and the incidence rate of 0.05, we can say that “5% more women that acquired this credit card in the cohort did not pay on time due to the system”. 

## D&M 
Distribution of live (or new) data may be different from training data so the Silhouette score and PSI of input variables can also be monitored. We can ensure that the system’s monitoring and review regime ensures that the DSAI system’s impacts are aligned with its XRAI objectives through several review processes: 
- Selection pool before a marketing campaign is analyzed for any covariate shifts 
- Distributions of responses for each model during the campaign with respect to the product lift score are analyzed periodically (ex. every week, every x days) 
- Profitability and rejection lift rate should be estimated and reported to System Owners and Assessors periodically 

Some mechanisms for mitigating unintended harms to individuals arising from the system’s deployment are as follows: 
- Customers can be given the opportunity to rate the experience of their interventions, or opt out from future marketing interventions 
- Customer relations teams manage complaints about the products being campaigned 
- Customers could request information on why applications are rejected 
- Model interpretability can be embedded into models or dashboards to help product or application teams understand why decisions were made 