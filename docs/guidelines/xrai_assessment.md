---
layout: default
title: XRAI Assessment Process
parent: Guidelines
nav_order: 3
---

# XRAI Assessment Process
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Overall Process for Applying the XRAI Assessment Methdology
The scope of the XRAI Assessment methodology is defined by the XRAI Principles. According to these principles, “DSAI” refers to Data Science and Artificial Intelligence methods, which are defined as technologies that assist or replace human decision-making. Since DSAI systems refer to a broad set of techniques and have no standards definition across industries, institutions may establish internal definitions of applications in scope with their DSAI risk management framework. 

However, some systems identified as DSAI may have low XRAI risks, and hence do not meet the institution’s threshold for conducting XRAI or risk assessments. Such systems include simple automation tasks such as uploading, downloading, and renaming files, or auto-sending of receipts or emails. This is likely true of systems not in production, or for which robust risk management processes that encompass XRAI principles are already in place. Thus, the institution should determine which systems are in scope based on the identified level of risk associated with each unique AIDA system. 

The responsibility for conducting risk level assessment can vary and may be shared among multiple units depending on the type of system and DS teams involved. The validation process can be divided into two parts: quantitative and qualitative. Quantitative validation pertains to the performance metrics of the AI/ML model, while qualitative validation is guided through the model management scorecard. Some of the technical terms in this scorecard are the following: 
- **Backtesting** – it is used to assess the performance of a model by evaluating its predictions against historical data ([MathWorks](https://www.mathworks.com/help/finance/backtest-strategies-using-deep-learning.html)). 
- **Benchmarking** – the process of comparing the performance of a model against a predefined standard ([Dobrakowski & Kwiatkowska, 2022](https://www.mim.ai/what-is-a-benchmark-and-why-do-you-need-it/)). 
- **Data Clean-up** – the process of fixing or removing incorrect, corrupted, incorrectly formatted, duplicate, or missing data within a dataset ([Barkved, 2022](https://www.obviously.ai/post/data-cleaning-in-machine-learning)). 
- **Data Integrity** – refers to the accuracy, consistency, and reliability of all the data within the dataset ([Paka, 2021](https://towardsdatascience.com/why-data-integrity-is-key-to-ml-monitoring-3843edd75cf5)). 
- **Maker-Checker Process** – it is a workflow mechanism where every change made by system developers is reviewed and approved before being finalized ([Singh, 2023](https://www.linkedin.com/pulse/implementation-maker-checker-4-eyes-principle-ajendra-singh/)). 
- **Manual Override** – a process of human agent taking control of an automized system. 
- **Model Risk Management** – refers to the supervision of risks from the potential adverse consequences of decisions based on incorrect or misused models ([Agarwala et. al., 2020](https://www.ey.com/en_us/banking-capital-markets/understand-model-risk-management-for-ai-and-machine-learning)). 
- **Model Theory** – refers to a systematic framework used for the development, implementation, and validation of a model ([Chase & Freitag, 2018](https://arxiv.org/abs/1801.06566)). 
- **Process Manuals** – refer to the step-by-step procedures for executing various processes within an organization. 
- **RAG (Red, Amber, Green) Status** - a simple visual indicator used to communicate the current state of a system. Green signifies a favorable condition while Red signifies the opposite ([Greany, 2022](https://www.gatekeeperhq.com/blog/how-to-use-rag-status-in-contract-management)). 
- **Sensitivity Analysis** – the process of analyzing how the target variable is affected based on changes in other features ([Faraj, 2020](https://towardsdatascience.com/the-sensitivity-analysis-a-powerful-yet-underused-tool-for-data-scientists-e553fa695976)). 
- **Stress Testing** – refers to the evaluation process used to assess the resilience and stability of a model under extreme conditions ([MathWorks](https://www.mathworks.com/help/risk/interpret-and-stress-test-deep-learning-network-for-probability-default.html)). 
- **System Maintenance** – regular check and monitoring of a system to ensure its optimal functioning, reliability, and longevity. 
- **User Acceptance Testing (UAT)** – the process of checking whether the built system follows users’ requirements defined during the development of the project plan ([Simplilearn, 2023](https://www.simplilearn.com/what-is-user-acceptance-testing-article)).  

## Assessing the risk level of the DSAI system 
The risk assessment is to evaluate the overall likelihood of risk occurring by utilizing risk tiering. This should aim to place the DSAI system into a specific risk tier or level such as “low”, “moderate”, or “high”. The goal of risk tiering is to determine the risk tolerance level and to ensure that models with similar levels of risk are treated similarly. In addition, this will allocate more assessment resources to higher risk systems through appropriate customizations of the XRAI methodology, rather than directly quantifying risk alone.  

The final risk assessment will be determined by combining model interpretation with evaluation of the associated risks. This involves identifying the factors that will influence the model’s prediction and assessing the severity and likelihood of those risks. We suggest the following categories to be used in risk assessment. Each team can also include any other ethical or legal implications depending on the use case. 
- **Extent to which the DSAI system is used in decision-making** – a complete substitution of a DSAI system for human decision-making may increase the risk of accidental systematic disadvantage 
- **Complexity of the DSAI model** – more complex models may obscure the ways in which personal data or other attributes is used 
- **Extent of automation of process of DSAI-driven decision-making** – more automation is likely to mean a higher volume and/or speed of DSAI-driven decision-making, which may increase scope of impact and decrease opportunities for timely human intervention to prevent issues 
- **Severity of impact on internal stakeholders** ([Personal Data Protection Commission Singapore, 2022](https://www.pdpc.gov.sg/-/media/Files/PDPC/PDF-Files/Resource-for-Organisation/AI/SGModelAIGovFramework2.pdf)) – the computation of severity and probability of impact will depend on the use case; for example, the use of DSAI systems to make credit approval or pricing decisions is more consequential than adjusting marketing messages  
- **Probability of impact on internal stakeholders** ([**Personal Data Protection Commission Singapore, 2022](https://www.pdpc.gov.sg/-/media/Files/PDPC/PDF-Files/Resource-for-Organisation/AI/SGModelAIGovFramework2.pdf)) – The probability of impact to stakeholders may be high or low depending on the efficiency and efficacy of the DSAI systems. High severity of harm does not mean there is a high likelihood of the incident occurring.   
- **Severity of impact on external stakeholders** – see above 
- **Probability of impact on external stakeholders** – see above 
- **Monetary and financial impact** – DSAI models may be of higher risk because of potential impact to P&L 
- **Regulatory impact** – DSAI models may be of higher risk because of regulatory exposure of their decision-making, such as phishing or mule detection 
- **Options for recourse available** – if there are efficient and effective ways for customers or other stakeholders to challenge or change DSAI system’s decisions, then the associated risks may be lower 

A sample table below is provided as a template for assessing the risk level for XRAI methodologies. Identifiers and conditions that will contribute to each risk category, including human behavior, data privacy/ security issues, environment conditions, technical failures, etc. must be stated in “Related Risks”, so that “Risk Level” can be properly labelled as “Low”, “Medium”, or “High”. A comprehensive assessment will help to effectively manage and mitigate risks, when they occur. This table is also accessible via document in our [GitHub repo](https://github.com/gaberamolete/toolkit-xrai/blob/main/Risk%20Assessment%20for%20XRAI%20Methodology.docx).

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  overflow:hidden;padding:10px 5px;word-break:normal;}
.tg th{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  font-weight:normal;overflow:hidden;padding:10px 5px;word-break:normal;}
.tg .tg-0pky{border-color:inherit;text-align:left;vertical-align:top}
.tg .tg-0lax{text-align:left;vertical-align:top}
</style>
<table class="tg">
<thead>
  <tr>
    <th class="tg-0pky" colspan="5">Risk Assessment for XRAI Methodology - &lt;DSAI System Name&gt;</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0pky" rowspan="2">Risk Category</td>
    <td class="tg-0pky" rowspan="2">Related Risks</td>
    <td class="tg-0pky" colspan="3">Risk Level</td>
  </tr>
  <tr>
    <td class="tg-0pky">Low</td>
    <td class="tg-0pky">Medium</td>
    <td class="tg-0pky">High</td>
  </tr>
  <tr>
    <td class="tg-0pky">Extent to which the DSAI system is used in decision-making </td>
    <td class="tg-0pky"></td>
    <td class="tg-0pky"></td>
    <td class="tg-0pky"></td>
    <td class="tg-0pky"></td>
  </tr>
  <tr>
    <td class="tg-0lax">Complexity of the DSAI model</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">Extent of automation of process of DSAI-driven decision-making</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">Severity of impact on internal stakeholders </td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">Probability of impact on internal stakeholders</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">Severity of impact on external stakeholders</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">Probability of impact on external stakeholders</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">Monetary and financial impact</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">Regulatory impact</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">Options for recourse available</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax" colspan="2">FINAL RISK ASSESSMENT</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
  </tr>
</tbody>
</table>

Here is an example of the risk assessment table being used for an auto loan application use case.

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  overflow:hidden;padding:10px 5px;word-break:normal;}
.tg th{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  font-weight:normal;overflow:hidden;padding:10px 5px;word-break:normal;}
.tg .tg-lto5{background-color:#f8a102;border-color:inherit;text-align:left;vertical-align:top}
.tg .tg-0pky{border-color:inherit;text-align:left;vertical-align:top}
.tg .tg-fymr{border-color:inherit;font-weight:bold;text-align:left;vertical-align:top}
.tg .tg-uog8{border-color:inherit;text-align:left;text-decoration:underline;vertical-align:top}
</style>
<table class="tg">
<thead>
  <tr>
    <th class="tg-0pky" colspan="5"><span style="font-weight:bold;text-decoration:underline">Risk Assessment for XRAI Methodology - Auto Loan Application</span></th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-fymr" rowspan="2">Risk Category</td>
    <td class="tg-fymr" rowspan="2">Related Risks</td>
    <td class="tg-fymr" colspan="3">Risk Level</td>
  </tr>
  <tr>
    <td class="tg-uog8">Low</td>
    <td class="tg-uog8">Medium</td>
    <td class="tg-uog8">High</td>
  </tr>
  <tr>
    <td class="tg-0pky">Extent to which the DSAI system is used in decision-making </td>
    <td class="tg-0pky">- Output of model gives recommended decision to loan officer and key features <br>- Still up to loan officer whether to follow the DSAI system or not </td>
    <td class="tg-lto5"></td>
    <td class="tg-0pky"></td>
    <td class="tg-0pky"></td>
  </tr>
  <tr>
    <td class="tg-0pky">Complexity of the DSAI model</td>
    <td class="tg-0pky">- Takes in data from Eclipse software used for processing loan applications <br>- Uses personal data (ex. Gender, age group, income level) to make decisions <br>- Showcases XRAI graphs </td>
    <td class="tg-0pky"></td>
    <td class="tg-0pky"></td>
    <td class="tg-lto5"></td>
  </tr>
  <tr>
    <td class="tg-0pky">Extent of automation of process of DSAI-driven decision-making</td>
    <td class="tg-0pky">- Models are updated quarterly as scheduled, but with intervention from data scientists if thresholds are not met <br>- Recommendations are requested and made per individual, but loan officers still have final say </td>
    <td class="tg-lto5"></td>
    <td class="tg-0pky"></td>
    <td class="tg-0pky"></td>
  </tr>
  <tr>
    <td class="tg-0pky">Severity of impact on internal stakeholders </td>
    <td class="tg-0pky">- If a false positive decision is made (approved then defaults), then bank stands to lose more money <br>- If a false negative decision is made (rejected but ok buyer), no monetary loss but potential customer loss </td>
    <td class="tg-0pky"></td>
    <td class="tg-lto5"></td>
    <td class="tg-0pky"></td>
  </tr>
  <tr>
    <td class="tg-0pky">Probability of impact on internal stakeholders</td>
    <td class="tg-0pky">- The probability of a false positive decision occurring is low/ high depending on model being developed and utilized. </td>
    <td class="tg-0pky"></td>
    <td class="tg-lto5"></td>
    <td class="tg-0pky"></td>
  </tr>
  <tr>
    <td class="tg-0pky">Severity of impact on external stakeholders</td>
    <td class="tg-0pky">- If a false positive decision is made (approved then defaults), customer is on look-out from the bank and other financial institutions <br>- If a false negative decision is made (rejected but ok buyer), no monetary loss but customer may have lessened relationship status with bank <br>- Loan applicant does not get explanation of application result regardless of approved or rejected </td>
    <td class="tg-0pky"></td>
    <td class="tg-lto5"></td>
    <td class="tg-0pky"></td>
  </tr>
  <tr>
    <td class="tg-0pky">Probability of impact on external stakeholders</td>
    <td class="tg-0pky">- The probability of a false negative decision occurring is low/ high depending on model being developed and utilized. </td>
    <td class="tg-0pky"></td>
    <td class="tg-lto5"></td>
    <td class="tg-0pky"></td>
  </tr>
  <tr>
    <td class="tg-0pky">Monetary and financial impact</td>
    <td class="tg-0pky">- The bank loses more money if the DSAI model helps a loan officer approve a rejectable applicant </td>
    <td class="tg-0pky"></td>
    <td class="tg-lto5"></td>
    <td class="tg-0pky"></td>
  </tr>
  <tr>
    <td class="tg-0pky">Regulatory impact</td>
    <td class="tg-0pky">- None known </td>
    <td class="tg-lto5"></td>
    <td class="tg-0pky"></td>
    <td class="tg-0pky"></td>
  </tr>
  <tr>
    <td class="tg-0pky">Options for recourse available</td>
    <td class="tg-0pky">- Loan officers still have final say on loan application decision <br></td>
    <td class="tg-lto5"></td>
    <td class="tg-0pky"></td>
    <td class="tg-0pky"></td>
  </tr>
  <tr>
    <td class="tg-fymr" colspan="2">FINAL RISK ASSESSMENT</td>
    <td class="tg-0pky"></td>
    <td class="tg-lto5"></td>
    <td class="tg-0pky"></td>
  </tr>
</tbody>
</table>

Different kinds of risks are also present during the modelling of the AI/ML system itself. These include: 
- **Unclean Data** (Is data used unclean?): Unclean data will generate abrupt output as the data may not be adequately understood by the model. Unclean data involves errors, outliers, and unstructured data ([Redman, 2018](https://hbr.org/2018/04/if-your-data-is-bad-your-machine-learning-tools-are-useless)). 
- **Overfitting** (Does the model performed poorly with unseen data?): An overfitting model fits the training data so perfectly that it was not able to learn the variability for the algorithm. Hence, when tested on the testing data, the performance is quite bad ([IBM](https://www.ibm.com/topics/overfitting)). 
- **Biased Data** (Is the data biased towards certain groups within the dataset?): Biased data may indirectly make the model discriminate against unprivileged groups in the dataset ([DeBrusk, 2018](https://sloanreview.mit.edu/article/the-risk-of-machine-learning-bias-and-how-to-prevent-it/)). 
- **Security Risks** (Do the model used personal information as input data?): The data used in building the model can be exposed to security risks by malicious attackers, which might cause any personal information included to be leaked to attackers. Attacks include poisoning, evasion, unintentional memorization ([Weis, 2019](https://sweis.medium.com/security-privacy-risks-of-machine-learning-models-cd0a44ac22b9)). 
- **Poor Problem-Solution Alignment** (Is the AI/ML model appropriate to the problem?): Choosing the right ML model is important in every AI/ML-related task. Implementing an overly complicated model (e.g., deep learning models) on simple tasks is inefficient ([Cohen, 2020](https://insights.sei.cmu.edu/blog/three-risks-in-building-machine-learning-systems/)). 
- **Unexpected Behavior and Unintended Consequences** (Do you test the model for any unexpected behavior?): ML models can exhibit unexpected behavior that may lead to unintended consequences when deployed in the real world. Examples include vulnerability to adversarial examples, interactions between ML models and software systems, feedback loops which can propagate biases in training data, and others ([Cohen, 2020](https://insights.sei.cmu.edu/blog/three-risks-in-building-machine-learning-systems/)). 

## Applying the Methodology 
The figure below is an example of how a DSAI team might use the XRAI Methodology. This does not explain the Methodology itself, but rather how it is utilized on a larger, project-making scale. A flowchart is also provided. 
1. The DSAI System Owner to conduct Risk Assessment to determine appropriate customization of the Methodology 
2. The DSAI System Owner provides summary to DSAI System Assessor (based on risk level), to refine scope of the assessment 
3. The DSAI System Owner and Developers undergo Preprocessing, Analysis, Modelling 
4. The DSAI System Assessor judges system’s alignment with XRAI principles, after system results are presented by the Owners and Developers 
5. After feedback, the DSAI System Owner works with the Developers to make changes 
6. After revisions, the DSAI system results can now be shared with external stakeholders 

![](../../assets/images/assessment_01-flowchart.png)

## Integrating the XRAI Methodology with Existing Risk Management
Outside of the XRAI Methodology exists multiple DSAI risk management practices across a multitude of industries, yet a common standard for applying these elements have not particularly been established, as institutions may be at different maturity stages in adopting and specifying risk management processes to DSAI systems. The following section aims to highlight common observations across elements of risk management for DSAI systems in corporate settings. 

### Initiation stage 
Regularly, an institution has a cohesive identification of applications in the DSAI risk management framework. DSAI systems are captured in existing or newly established model inventory management processes. In addition to documentation standards, elements such as retraining frequency and data input type are defined. 

Once identified, the institution should perform an assessment of risks associated with the DSAI system based on pre-defined criteria. While varying in name, these criteria cover three dimensions:  
- **Complexity** – mathematical computation, number and type of data sources, computing resources used, level of human intervention needed with the DSAI system 
- Materiality – the regulatory, economic, social, end-user consequences associated with a potential error of the DSAI system (e.g. reputation, financial, etc.), the number of users applying the DSAI system, the possibilities of recourse 
- **Impact** – consequentiality of decisions based using the DSAI system, the volume and scope of usage, the type and number of stakeholders affected, probability and severity of harms that can be caused 

DSAI systems can be categorized into risk tiers associated with specific requirements depending on the severity of these dimensions. Such requirements can include: 
- Level of required documentation 
- Required approval level for model use, model deployment, or model revisions 
- Monitoring frequency and depth 
- Defined escalation procedures 
- Controls framework in various lifecycle stages 
- Validation activities like frequency and depth 

Such tiers should be defined by the DSAI System Assessor, who is likely a governance or risk management team. 

### Development stage 
Data plays a key role in the output of DSAI systems. Thus, data acquisition and processing take on a greater importance, so institutions are enhancing their control frameworks and considerations of relevant constraints, like personal data usage and data quality. 

Institutions are also emphasizing the explainability of DSAI systems to ensure that they operate in a manner consistent with their business and end-user purpose. This includes how the business problem statement is addressed with a designated system, the reasoning behind choices made in system design, and how system results are showcased. This may include discussions on possible trade-offs between accuracy and interpretability of the system’s outputs. 

### Review stage 
Model review is a key component of the model lifecycle and is reflected in established governance frameworks. The model’s fitness for purpose is documented in development and review. Explainability once again has a key role in effective review, especially as the traceability between model inputs and outputs decreases in increasing DSAI system complexity. These can include the establishment of model validation teams, or the use of technological support to standardize validation tasks and concentrate human efforts on interpretation. 

### Ongoing monitoring 
Periodic reviews of AI models are typically applied as a standard to determine whether DSAI systems continue to be fit for purpose given availability of new data or potential changes to environments. Monitoring frequency is linked to the risk tiering of the DSAI system and the model type. For example, a supervised ML model with infrequent batch updates may require testing semi-annually, but a reinforcement learning model receiving continuous feedback may require testing monthly. 

Active changes to a DSAI system’s components such as models, inputs, outputs, or production infrastructure are typically monitored for potential impacts to the system’s operation. These dynamics cause continuous changes, requiring increased scrutiny. The system should be robust and not impacted by retraining or incorrect training data.  