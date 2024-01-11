---
layout: default
title: XRAI Principles
parent: Guidelines
nav_order: 1
---

# XRAI Principles
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

Explainable and Responsible AI (XRAI) is a blanket term of multiple concepts related to how DSAI systems should be created while achieving technical excellence.  Inspired by the work of the [Monetary Authority of Singapore](https://www.mas.gov.sg/~/media/MAS/News%20and%20Publications/Monographs%20and%20Information%20Papers/FEAT%20Principles%20Final.pdf) and the [Infocomm Media Development Authority (IMDA)](https://www.imda.gov.sg/), we hope to define a set of principles that data scientists from Aboitiz Data Innovation (ADI) can use while developing and deploying their DSAI models. These principles, which will be described in further detail, are the following: 
- Transparency 
- Explainability 
- Repeatability / Reproducibility 
- Safety & Security 
- Robustness 
- Fairness 
- Data Governance 
- Accountability 
- Human Agency and Oversight 
- Inclusive Growth, Societal & Environmental Well-being (Ethics) 

If there is an existing set of established principles such as FEAT that are already being used by AIDA/DSAI systems, what then is XRAI and why do we need to define a separate term? We posit that XRAI concepts can be applied to AIDA/DSAI systems not limited to the financial services domain. To elevate the effectiveness of DSAI models in the fields that Aboitiz has expertise in – such as power, real estate, construction, assets, food – similar guidelines and tools should be made that are inclusive to the needs of these domains. A broader Framework such as this should be developed so that all models that ADI create will not be prone to excessive bias or other XRAI-related inconsistencies. 

With this, we define three (3) XRAI-based intervention stages. These are arbitrary phases encompassing the Data Science pipeline by which XRAI principles can be applied differently: 
- **Input** – Data preparation and understanding, inputs to model, extraction, preprocessing, what data to include, data quality. This includes synthetic data, and any intermediate features (in an intermediate layer in a neural network)  
- **Model and Output (M&O)** -- development, initial results/output of model and interpretation  
- **Deployment and Monitoring (D&M)** – sharing to stakeholders, dashboard and input to business process 

As proposed by the IMDA, the Explainable and Responsible AI (XRAI) principles can be grouped into five (5) pillars:  
- Transparency on the use of AI and AI Systems 
- Understanding how DSAI System reaches a Decision 
- Safety and Resilience of AI Systems 
- Fairness/ No Unintended Discrimination 
- Management and Oversight of AI System 

These pillars hold previously mentioned XRAI principles. We will also be looking at each principle on its viability through each XRAI-based intervention stage: Input, Model and Output (M&O), and Deployment and Monitoring (D&M). We describe technical tests that can be employed throughout each intervention stage. Do note that not all principles have technical tests applicable at each stage; we will be mentioning this in its specific section. 

## Transparency on use of AI and AI Systems 
Appropriate info is provided to individuals impacted by AI system. A better word is ‘apparent’, as in, readily understood and not hidden (within a black box). 

### Transparency
The implementation of AI in the system will be disclosed to end-users. Empowered individuals can make an informed decision if they want to use the AI-enabled system. 
- **Input**: No technical tests are seen to be applicable for this XRAI principle at this stage for System Developers, although transparency can be practiced in data collection stage especially when collecting data from surveys or mobile applications. 
- **M&O**: No technical tests are seen to be applicable for this XRAI principle at this stage, but it should be clear to DSAI System Owners and Assessors what features found in the data are and are not being used and transformed. 
- **D&M**: Data collection policies should be transparent to alleviate concerns related to AI. Process checks of documentary evidence (such as company policy and communication collaterals) of providing appropriate information to users who may be impacted by the AI system. The information can include, under the condition of not compromising IP, safety, and system integrity, use of AI in the system, intended use, limitations, and risk assessment.  

## Understanding how DSAI System reaches a decision 
Ensuring AI operation/results are explainable, accurate and consistent. This enables users to know the factors contributing to the AI model’s output (decision/recommendation).  

### Explainability 
Explainability refers to the concept that the end user can understand why a prediction is made by an AI system. Global explanation methods attempt to explain the model behavior while local explanation methods focus on explaining an individual prediction. 
- **Input**: These are the constituent features used in the model that are being explained and presented in a data dictionary. This also includes explanations with respect to an intermediate layer of the network. Internal explanations are necessary for models with an inherent structure that is sequential, such as intermediate layers of a neural network ​(Leino et al., 2018)​ or branching structures within decision trees (using Information gain to understand the variable where it was split). 
- **M&O**: Interpretable models are machine learning (ML) models with a simple structure (such as sparse linear models or shallow decision trees) that can ‘explain themselves’ i.e., are easy for humans to interpret. Post-hoc explanation and counterfactual methods can analyze and explain a relatively more complex ML model after it has been trained.  
- **D&M**: This assesses the impact of features on model outcomes to stakeholders. Example is Partial Dependence Plots (DPD) which provides visual interpretation of marginal chances in model outputs when a feature is changed. Process checks include verifying documentary evidence of considerations given to the choice of models, such as rationale, risk assessments, and trade-offs of the model.  

### Repeatability / Reproducibility 
AI results are consistent, and can be replicated by the owner, developer, or another third party.  
- **Input**: Ensure that any attempts to randomize or stratify data during splitting are done with set seeds. 
- **M&O**: Ensure that model files are saved with specified parameters and can be linked to clear datasets. Create a requirements.txt file or similar file that documents the necessary packages needed to run files on programming languages. Another good practice is to ensure that preprocessing steps or other methodologies applied to the dataset and model creation are documented well. 
- **D&M**: Assess through process checks of documentary evidence including evidence of AI model provenance, data provenance and use of versioning tools. 

## Safety and Resilience of AI Systems 
This principle states that the AI system should be reliable, performs as intended, and will not cause harm.  

### Safety and Security 
AI system is safe. Conduct impact and risk assessment. Known risks have been identified and/or mitigated. 
- **Input**: No technical tests are seen to be applicable for this XRAI principle at this stage. However, should the data contain any private and personally identifiable data, it will be explored through company-specified environments and platforms such as CDSW or Databricks. 
- **M&O**: See above. 
- **D&M**: Assess through process checks of documentary evidence of materiality assessment and risk assessment, including how known risks of the AI system have been identified and mitigated.  

### Robustness 
This assesses whether the AI system can still function despite unexpected inputs. Model robustness refers to the degree that a model’s performance changes when using new data versus training data. Ideally, performance should not deviate significantly.  
- **Input**: This refers to data quality, which is the accuracy, completeness and clarity of the data being used to train the model.  
- **M&O**: Technical tests attempt to assess if the model performs as expected even with unexpected inputs.  
- **D&M**: Process checks include verifying documentary evidence, review of factors that may affect the performance of the AI model, including adversarial attacks.  

## Fairness / No Unintended Discrimination 
### Fairness 
End-users need to know that the training data is reflective of the characteristics of the population being analysed. An AI system will be considered biased if it discriminates against certain features or groups of features. This provides an opportunity to address biases by detecting them and measuring them at each stage of the ML lifecycle.  
- **Input**: The training data may not have sufficient representation of various feature groups or may contain biased labels.  This imbalance can conflate the bias measure, and our models may be more accurate in classifying one class than in the other. We need to choose bias measures that are appropriate for the application and the situation. So, we want to utilize metrics that can be computed on the raw dataset before training.  
- **M&O**: Any bias that arises post-training may emanate from biases in the data and/or biases in the model’s classification and prediction. Models built on biases would reproduce or exacerbate those biases during predictions in each stage of the ML cycle. After training the ML model, we gain more information from the model itself, particularly the predicted probabilities from it and the predicted labels. These allow an additional set of bias metrics to be calculated and analyzed.  
- **D&M**: It is quite possible that after the model has been deployed, the distribution of the data that the deployed model sees, that is, the live data, is different from that of the training dataset. This change, also known as concept drift, may cause the model to exhibit more bias than it did on the training data. The change in the live data distribution might be temporary (e.g., due to some short-lived behavior like the holiday season) or permanent. In either case, it might be important to detect these changes. Same bias metrics during modelling can be monitored at continuous intervals. This frequency can be two days, a week, a month, etc. depending upon the Data Science team and the use case. 

### Data Governance 
Source and data quality should be sound. Good data governance practices should be in place when training AI models. 
- **Input**: No technical tests are seen to be applicable for this XRAI principle at this stage. 
- **M&O**: No technical tests are seen to be applicable for this XRAI principle at this stage. 
- **D&M**: We need to hold ourselves accountable when deploying AI applications, especially when users are concerned about how we access and use confidential information. The two takeaways are segmentation and visibility. We must ensure we can monitor and restrict how our models use data at all stages. Segmentation prepares and mitigates the impact of a breach to keep user information and data as safe as possible. Also, data collection policies should be transparent to alleviate concerns related to AI. Taking a strong approach towards maintaining high privacy and governance standards will further ensure we are legally compliant.  

## Management and Oversight of AI 
Ensure human accountability and control, and that the AI-enabled system is developed for the good of humans and society. 

### Accountability 
Proper management oversight of AI system development 
- **Input**: No technical tests are seen to be applicable for this XRAI principle at this stage. 
- **M&O**: No technical tests are seen to be applicable for this XRAI principle at this stage. 
- **D&M**: Assess through process checks of documentary evidence, including evidence of clear internal governance mechanisms for proper management oversight of the AI system’s development and deployment. 

### Human Agency and Oversight 
AI system designed in a way that will not decrease human ability to make decisions. 
- **Input**: No technical tests are seen to be applicable for this XRAI principle at this stage 
- **M&O**: No technical tests are seen to be applicable for this XRAI principle at this stage. 
- **D&M**: Assess through process checks of documentary evidence that AI system is designed in a way that will not reduce human’s ability to make decision or to take control of the system. This includes defining the role of humans in its oversight and control of the AI system such as human-in-the-loop, human-over-the-loop, or human-out-of-the-loop.  

### Inclusive Growth, Societal, and Environmental Wellbeing (Ethics) 
Beneficial outcomes for people and planet. As with the concept’s nature, there are no standard technical tests nor process checks that can be made readily available. However, DSAI System Developers and Owners should take steps to critically consider such factors despite not being of a technical nature.  
- **Input**: No technical tests are seen to be applicable for this XRAI principle at this stage.  
- **M&O**: No technical tests are seen to be applicable for this XRAI principle at this stage. 
- **D&M**: Pre-deployment assessment forms given by privacy authorities should contain guiding questions on the ethics and potential holistic risks arising from the model’s outcomes. 