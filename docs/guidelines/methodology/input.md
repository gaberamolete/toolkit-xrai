---
layout: default
title: Input
parent: XRAI Methodology
grand_parent: Guidelines
nav_order: 1
---

# XRAI Methodology - Input
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

### System Objectives and Context 
Before dealing with data, it is extremely important to understand the DSAI System’s objectives and contexts so as to spot potential XRAI-related interventions or stages where disadvantages can occur or stem from. We suggest some guide questions to help DSAI System Developers and Owners know the goals and limitations of the possible DSAI System solution. 
- What are the system objectives? What are the milestones or key performance indices (KPIs)? What are the business goals? What are the regulations imposed by our company or other regulatory bodies? 
- Who are the protected segments or disadvantaged groups? 
- What are the potential harms and benefits created by system’s operations? 
- What are the XRAI objectives of the system with respect to protected segments and the harms/ benefits imposed on those segments? 

Usually when dealing with datasets, there may be groups or segments that are underrepresented and that can be disadvantaged when a model is trained for prediction. For example, certain age or ethnic groups may be disadvantaged in application models due to their lack of prevalence in datasets. In general, we should always consider any potentially disadvantaged groups that should be protected. 

### How to define a good problem statement for machine learning
What is a problem statement? We can describe it as a clear statement describing the initial state of a problem that's to be solved. The statement indicates problem properties such as the task to be solved, the current performance of existing systems and experience with the current system. 

According to an article on [Towards Data Science (Alake, 2020)](https://towardsdatascience.com/how-to-approach-problem-definition-in-your-next-deep-learning-project-9d76960932b4), conducting a successful problem definition process within a machine learning or deep learning project involves a fundamental analysis and evaluation of what, why and how aspects associated with the problem. Coming up with a good problem definition is usually an iterative process. It can reveal more questions and items to consider that would have gone neglected without going through a problem definition process. 

The questions included below act as guiding beacons that enable a thorough analysis of a problem and surrounding topics. 
1. What is the nature of the problem that requires solving? 
2. Why does the problem require a solution? 
3. How should solutions to the problem be approached? 
4. What aspect of the problem will a deep learning model solve? 
5. How is the solution to the problem intended to be interacted with? 

Well-written problem definitions are free of ambiguous statements and are not subject to misinterpretations due to the clear and concise description of the problem. 

Below are some examples of problem definitions associated with tasks solved through deep learning techniques. 

> Example 1: “Reduce the time taken to come up with a creative and original image caption that goes with an Instagram image post.” 
> 
> Example 2: “Automate the generation of stock recommendations and price predictions for investors based on the previously recorded historic 5-year price movement of stocks within the SNP 500.” 

<u>1. What is the nature of the problem that requires solving?</u>
Understanding the nature of a problem provides insight into components and attributes of the yet to be implemented solutions. A good understanding of a problem guides future decisions to make at the later project stages, especially decisions such as determining if a deep learning solution is even feasible. 

In example 1, one can understand the nature of the problem by looking into the environment the problem resides in (Instagram). Awareness of any technical mentions (Image captioning) or phrases describing existing processes associated with the problem also provides insight into its nature.

Example 1’s defined problem is concerned with mainly the reduction of the time(“Reduce the time”) it takes to complete a task (Image captioning). 

<u>2. Why does the problem require a solution? </u>

Answering these guiding questions will require more than just problem statements. To answer why a problem requires a solution will involve a dialogue with project stakeholders, more specifically, the individual(s) that are currently experiencing the problem. 

Understanding why a problem requires a solution will indicate the urgency and importance of a solution. Knowing how urgent a solution is required for a problem can direct the approach of solution implementation. Deep Learning approaches are notorious for having extensive training and evaluation times. 

It might be more useful to implement a heuristic-based approach to solving a problem that takes hours to implement and test as opposed to spending days or weeks training and fine-tuning the machine/deep learning model. 

<u>3. How should solutions to the problem be approached? </u>

Likely, the answer to this question is already becoming more evident from answering ‘why a solution is required’ in the first place. There is more than one way to approach a deep learning-based solution. 

At a high level, most machine learning practitioners understand that ML models can be classified based on the following categories: supervised, unsupervised and semi-supervised learning approaches. At times it is more pragmatic to implement a solution with a simple ML model and iteratively improve on the model after the user has a version of a proposed solution in hand. 

<u>4. What aspect of the problem will a deep learning model solve? </u>

When exploring this question is always good to understand the limitations of deep learning-based solutions. Deep learning is good, but it can’t be leveraged to solve every problem. 

Deep learning solutions are well suited for problems that involve a quantifiable form of data in a repeating pattern; typically, these are in the form of text, images, audio or numeric data. In many cases, deep learning models are simply a smaller part to a more comprehensive solution. When thinking of solutions, it is common to make the assumptions of a single application that solves a problem. In more established domains and businesses, it is typical to find an ecosystem of applications and hardware devices communicating and operating in either a synchronous or asynchronous manner, to achieve a specific task. 

Understanding what aspect of a problem deep learning techniques will solve enables the scoping of the technical and time resource to allocate to a specific project, from a deep learning perspective. 

<u>5. How is the solution to the problem intended to be interacted with? </u>

Websites, mobile applications, desktop applications, these are various software forms that deep learning solutions can reside in, and each form requires a different level of interaction. Before diving solution delivery and deployment, it is essential to understand how interactions with the solution are conducted. 

Here are some key areas to focus on when answering this question: 
- How frequently is the solution going to be used by the user? Answering this at an early stage within a project lifecycle creates an opportunity to begin the scoping of model inference cost associated with model deployment. 
- Does the user of the solution require a result immediately when utilizing the functionalities of the implemented solution? 
- Give enough attention to the design and user interface of the implemented solution. 

### Is a Data Science system necessary?  
Determining if a Data Science system is necessary for different use cases is a pivotal step in data-driven decision-making. This assessment ensures that precious resources, including time, and budget, are invested wisely. By establishing a process of determination, DS teams can avoid embarking on unnecessary or ineffective projects but also maximize the potential for them to deliver tangible value, making it an essential step of the XRAI process. See Figure 1 for a flowchart of a typical assessment process. 

<u>Data Science System Assessment Process</u>
1. Problem Scoping and Goal Setting: Clearly define the problem, objectives, and expected outcomes. Establish key performance indicators (KPIs) that will measure the success of the project. 
2. Data Assessment: Evaluate the availability, quality, and relevance of data. Determine if the data can support the desired analyses and modeling. 
3. Cost-Benefit Analysis: Assess the potential benefits of implementing a Data Science system against the costs involved in terms of resources, time, and technology. 
4. Benchmarking: Compare the problem with existing solutions or traditional methods to determine if Data Science techniques offer significant advantages. 
5. Stakeholder Consultation: Involve relevant stakeholders, including domain experts and decision-makers, in the decision-making process to ensure alignment with business objectives. 
6. Risk Assessment: Identify potential risks related to data quality, model accuracy, ethical considerations, and legal compliance. 
7. Resource Availability: Determine if you have access to the necessary expertise (data scientists, engineers, etc.), computational resources, and tools. 

![](../../../assets/images/methodology-input_01-dssap.png)

### Dealing with Data 
#### Set a scope of the data what will be used 
Setting a well-defined scope of data usage is important in data science projects. It serves as the foundational blueprint for the entire endeavor, guiding every step from data collection to model deployment. This scope, carefully crafted and thoughtfully considered, determines what data will be harnessed, how it will be processed, and ultimately, what insights or solutions can be derived. Its importance lies in its ability to clarify objectives, allocate resources effectively, mitigate risks, address ethical considerations, maintain time efficiency, and enhance reproducibility. In essence, setting a data scope is the compass that guides a data science project towards success, ensuring that efforts are focused, ethical, and aligned with the objectives of the organization or problem at hand. 

#### Industry standards for scoping data 
1. CRISP-DM (Cross-Industry Standard Process for Data Mining): [CRISP-DM](https://www.sciencedirect.com/science/article/pii/S1877050921002416) is a widely accepted framework for data mining and data science projects. It consists of six phases: Business Understanding, Data Understanding, Data Preparation, Modeling, Evaluation, and Deployment. While it doesn't explicitly address setting the scope, it provides a structured approach to managing the entire data science project. 
2. TDSP (Team Data Science Process): Developed by Microsoft, [TDSP](https://learn.microsoft.com/en-us/azure/architecture/data-science-process/overview) is a framework for modern data science projects. It includes a specific phase called "Business Understanding and Framing" which emphasizes defining the problem, objectives, and scope of the project before diving into data analysis and modeling. 

#### Proposed Framework for Data Governance 
1. **Define Clear Data Ownership**: Assign data ownership roles and responsibilities to individuals or teams within the organization. Ensure accountability for data quality, security, and compliance. 
2. **Establish Data Governance Policies**: Develop and document data governance policies and standards. Cover data classification, security, privacy, quality, and compliance with relevant regulations. 
3. **Data Inventory and Catalog**: Create a comprehensive data inventory and catalog. Include metadata, data lineage, and details about data sources and usage. 
4. **Data Security and Privacy**: Implement robust data security measures, including access controls, encryption, and auditing. Ensure compliance with data privacy regulations and protect sensitive information. 
5. **Data Governance Training and Monitoring**: Provide data governance training to employees and regularly monitor adherence to policies. Continuously assess and improve data governance practices. 

#### Choosing what data to include
Feature selection is a process that chooses a subset of features from the original set of features to make the feature space optimally small, making the modeling process lighter. Some features can be readily filtered out, such as dates, ID numbers, URLs, and others. By common sense, these features provide no contribution to the prediction of the model. Moreover, other features that are also obviously related can be filtered out directly as these redundancies also do not provide a contribution to the model [(Tripathi, 2016)](https://www.linkedin.com/pulse/statistics-common-sense-two-things-data-science-cant-do-tripathi/). 

Popular techniques [(Bajaj, 2023)](https://www.geeksforgeeks.org/feature-selection-techniques-in-machine-learning/) for feature selection can generally be divided into three methods: filter methods, wrapper methods, and embedded methods. The filter method selects features from the dataset irrespective of the ML algorithm used. Some techniques under this method are: 
- **Information Gain** – measures the amount of information provided by each feature in arriving at the target value. Eliminate non-contributing features. To measure information gain, you can use the scikit-learn's `mutual_info_classif` function. 
- **Chi-Square Test** – tests the relationship between categorical variables. Eliminate closely related variables. Chi-Square Test is available in the Stability part of the toolkit. 
- **Fisher’s Score** – selects each feature independently according to their scores under Fisher criterion leading to a suboptimal set of features. Fisher’s Score is also available in the Stability part of the toolkit, but it is only applicable to classification cases 
- **Correlation Coefficient** – a measure of quantifying the association between the two continuous variables. Eliminate closely related variables. For regression cases, Pearson’s correlation coefficient is the most common measure, while Matthew’s correlation coefficient is the most common for classification. Both can be found in the scikit-learn library. 
- **Variance Threshold** – an approach where all features are removed whose variance doesn’t meet the specific threshold. This is available in the feature selection module of scikit-learn. 
- **Dispersion Ratio** – defined as the ratio of the arithmetic mean to that of geometric mean for a given feature. This feature selection is for clustering cases only, and one of the most common dispersion ratios would be the Calinski Harabaz score, which is also available in scikit-learn. 

On the other hand, the wrapper methods train the model using a portion of the features in an iterative manner. Based on the results, features are added/removed until we arrive in the best set of features that produced the best results. Some techniques under this method are: 
- **Forward Selection** – an iterative approach starting with an empty set of features and features which best improves our model after each iteration is added until the model no longer improves. 
- **Backward Elimination** – the opposite of forward selection, where the start is at the entire features, and iteratively eliminates the least significant feature, until the model performance no longer improves. 
- **Bi-directional Elimination** – combination of forward selection and backward elimination. This method, along with the forward selection and backward elimination, can be used through the SequentialFeatureSelector of scikit-learn. 
- **Exhaustive Selection** – considers all possible subset of the features, selecting the one that produces the best-performing result. For this method, we can use the `ExhaustiveFeatureSelector` from `mlxtend` library. 

Lastly, the embedded method blended the feature selection as part of the algorithm itself, like having a built-in feature selection in modelling. Some techniques under this method are:  
- **Regularization** – adds a penalty to different parameters of the model to avoid overfitting. L1 (Lasso) and L2 (Ridge) regularization are two of the most common regularization techniques that can be embedded to regression models. Both are available in scikit-learn library. 
- **Tree-based Method** – some ML algorithm like Random Forest or Gradient Boosting provides feature importance as a way to select features. Most of the time, this can be directly configured within the algorithm itself, especially for algorithms coming from the scikit-learn library. 

#### Test for (binary) classes in data 
Class imbalance refers to a situation where the number of examples belonging to one class is significantly smaller than the number of examples belonging to another class. For example, in a binary classification problem where one class represents a rare disease and the other class represents a healthy population, the number of positive examples (disease) may be much smaller than the number of negative examples (healthy), resulting in a class imbalance problem. 

To deal with class imbalance, several techniques can be used. One approach is to resample the dataset by either oversampling the minority class or undersampling the majority class. Another approach is to use cost-sensitive learning, where the cost of misclassifying the minority class is increased to account for the class imbalance. Additionally, different evaluation metrics, such as precision, recall, F1-score, and area under the receiver operating characteristic (ROC) curve, can be used to evaluate the performance of the model on the minority class. 

Examples of tests for class imbalance include proportions, Difference in Positive Proportions in Labels (DPL), KL divergence (KL), Jenson-Shannon divergence (JS), Lp-Norm (LP), Total variation distance (TVD), Kolmogorov-Smirnov (KS), Conditional Demographic Disparity in Labels (CDDL). 

For cases with multicategory labels, there are two approaches (a) collapse categories to binary and compute label imbalance measures. Or (b) compute label imbalances across all multiple categories. (a) is a special case, but it requires a human to examine and consider labels to be grouped and discover which ones are more significant.  

#### Errors, Biases, and other Properties in Data 
What errors, biases, properties in data used by system may impact system’s adherence to XRAI principles? Tools like [EvoML by TurinTech](https://github.com/EvoML/EvoML) perform data quality inspection and apply relevant techniques to ensure data is AI-ready. 
- **Sampling procedures** (i.e. unfair representation from previous data that is targeted, or presence of attrition that under-represents another long-term outcomes)  
- Systematic **errors in measurement**
- **Predictions from other models** used as data for a system  
- Data which **requires defining measurable proxies** (i.e. low socio-economic status by ‘earns less than X per annum’) 
- **Relevancy of the dataset**, since only attributes that provide meaningful information to the domain should be considered 
- **Accuracy of any labels/annotations**. This can be examined by recall or Intersection over Union (IoU). IoU has a range within [0,1] that provides the mean average precision, specifying the amount of overlap between predicted and ground truth.  
- **Size of the raw data corpus** (training, validation, test sets), since dataset size will depend on domain of the task, and complexity of the model. A point to note is also there is a threshold dataset size after which model performance plateaus.  
- **Variance of each class in data**, as the number of classes proportionally increase data size  
- **Type of classification** (e.g., are we predicting class for a data point, an entire image or each pixel in an image?) 
- **Comprehensiveness of the dataset**, since features used in the model should have enough samples of ‘edge’ cases for better generality during training 
- **Data representation due to change over time** (e.g., more customers are performing transactions in an app over time, than via a website) 