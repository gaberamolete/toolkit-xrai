---
title: Home
layout: default
nav_order: 1
description: The **DSAI Explainable and Responsible AI (XRAI) Toolkit** is a complementary tool to the [XRAI Guidelines document](https://unionbankphilippines.sharepoint.com/:b:/s/DataScienceInsightsTeam/EbGWZEJkn7REt1zzHspu-xABsLDpD1eD6mgHMjPJypnzdA?e=wm55U7). The Toolkit provides a one-stop tool for technical tests were identified by packaging widely used open-source libraries into a single platform, according to ADI/DSAI user needs. Hello!
permalink: /
---

<!-- This is a *bare-minimum* template to create a Jekyll site that uses the [Just the Docs] theme. You can easily set the created site to be published on [GitHub Pages] – the [README] file explains how to do that, along with other details.

If [Jekyll] is installed on your computer, you can also build and preview the created site *locally*. This lets you test changes before committing them, and avoids waiting for GitHub Pages.[^1] And you will be able to deploy your local build to a different platform than GitHub Pages.

More specifically, the created site:

- uses a gem-based approach, i.e. uses a `Gemfile` and loads the `just-the-docs` gem
- uses the [GitHub Pages / Actions workflow] to build and publish the site on GitHub Pages

Other than that, you're free to customize sites that you create with this template, however you like. You can easily change the versions of `just-the-docs` and Jekyll it uses, as well as adding further plugins.

[Browse our documentation][Just the Docs] to learn more about how to use this theme.

To get started with creating a site, simply:

1. click "[use this template]" to create a GitHub repository
2. go to Settings > Pages > Build and deployment > Source, and select GitHub Actions

If you want to maintain your docs in the `docs` directory of an existing project repo, see [Hosting your docs from an existing project repo](https://github.com/just-the-docs/just-the-docs-template/blob/main/README.md#hosting-your-docs-from-an-existing-project-repo) in the template README.

----

[^1]: [It can take up to 10 minutes for changes to your site to publish after you push the changes to GitHub](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll#creating-your-site).

[Just the Docs]: https://just-the-docs.github.io/just-the-docs/
[GitHub Pages]: https://docs.github.com/en/pages
[README]: https://github.com/just-the-docs/just-the-docs-template/blob/main/README.md
[Jekyll]: https://jekyllrb.com
[GitHub Pages / Actions workflow]: https://github.blog/changelog/2022-07-27-github-pages-custom-github-actions-workflows-beta/
[use this template]: https://github.com/just-the-docs/just-the-docs-template/generate -->

# Explainable and Responsible AI Toolkit
***Developed by AI&I COE***

The **DSAI Explainable and Responsible AI (XRAI) Toolkit** is a complementary tool to the [XRAI Guidelines document](https://unionbankphilippines.sharepoint.com/:b:/s/DataScienceInsightsTeam/EbGWZEJkn7REt1zzHspu-xABsLDpD1eD6mgHMjPJypnzdA?e=wm55U7). The Toolkit provides a one-stop tool for technical tests were identified by packaging widely used open-source libraries into a single platform, according to ADI/DSAI user needs. These tools include Python libraries such as `shap`, `dalex`, `dice-ml`, `alibi`, `netcal`, `aif360`, `scikit-learn`, and UI visualization libraries such as `raiwidgets` and `plotly`. This toolkit aims to: 
- Provide a user interface to guide users step-by-step in the testing process; 
- Support certain binary classification and regression models that use tabular data 
- Produce a basic summary report to help DSAI System Developers and Owners interpret test results 
- Intended to be deployable in the user’s environment

Subsequent versions and updates will be found in the XRAI [GitHub repo](https://github.com/aboitiz-data-innovation/XRAI), accompanied by XRAI Brownbag sessions.

# Introduction
## Assumptions / Limitations
The toolkit is in its third iteration of development. As such, there are limitations which hinders the Toolkit from being able to handle certain models and display other XRAI-related features. These include:
- Only Python users for V3. An R-based Toolkit may be released according to demand and necessity for later versions 
- This is mostly intended for classification and regression models; unsupervised models may run on some functions but are not guaranteed to work or provided correct insight.
- Certain features may be discussed in Guidelines V3 but are not yet in Toolkit V3
- This toolkit does not define ethical standards. It provides a way for DSAI System Developers and Owners to demonstrate their claims about the performance of their DSAI systems according to the XRAI principles

## Inputs
Our interactive toolkit only needs two main inputs before any major analysis:
- Model (.pkl or .sav)
- Data (train, test) (.csv) 

We intend for the user to have inputs mostly on the XRAI-related functions. However, we need the user to manually input **the names of train and test file**, in addition to target variable name. Prompts will be shown later in the notebook where you will need to load. In the shared folder we have provided sample model and data (test_data.csv, train_data.csv, finalized_model.pkl). For testing for different models and data you may just replace files.

## Features found in the Toolkit
- EDA – User-friendly, no-code custom visualizations to help you analyze your data's quality and distribution
- Fairness Preprocessing – Ready-made functions to clean and catch potential bias in data prior to model development
- Fairness Metrics – Find out which factors are disadvantaged by the model, and receive recommendations on how to mitigate unfairness
- Model Performance – Statistics of predicted outcome, dataset features, and error groups
- Local Explanations – Understand how a model affects individual explanations with a variety of techniques
- Global Explanations – Understand how a model is shaped
- Stability Analysis – OOT validation, data and model quality, how data and concepts decays over time
- Outlier Analysis – resampling, pre-model and post-model views
- What-if Analysis – counterfactual measures; showing how result for individual data point may change if one of its feature values was changed
- Robustness – Check if system can function despite unexpected inputs 
- Uncertainty – Models may not always make perfect predictions, and there can be some level of doubt or variability associated with their result

# Explainer Dashboard
A custom dashboard was developed to showcase the capabilities of the functions of the XRAI toolkit in an interactive and easy to understand environment, even for non-DS people. In order to run the dashboard, there are necessary steps to accomplish:
1. Dataset and Model Ingestion: Ensure that the model (.sav or .pkl) and dataset (.csv) is properly loaded. The `load_data_model` function from the `data_model` module provides a convenient way to do this.
2. Create an `explainerdashboard` explainer instance using the loaded model and test data. If this shows an error, this means that the model or data was not compatible with the `explainerdashboard` library. However, as the explainer instance won't really be used to extract data from, a dummy explainer can be built using sklearn's `LinearRegression` and an empty pandas' dataframes.
3. Extract the preprocessing pipeline in your model. Improper extraction of the preprocessing pipeline may lead to QII and SHAP components not working properly. Set to `None` if no preprocessing steps was present in the model pipeline.
4. Configure the groupings for the Grouped Variable Importance, if you want to analyze the variable importances on your dataset divided in a specific groupings.
5. Separate the continuous and categorical variables.
6. The model should be in a dictionary form, so set a name for the model as key, and the model itself as the value.
7. Select the `model_type` properly, either regression or classification. Incorrect assignment of this variable may lead to wrong components being displayed, which will not work since the `model_type` is not consitent with the model.
8. If the pipeline used was made thru sklearn, set `is_sklearn_pipe` to True, otherwise False.
9. Create a Dalex explainer object, which will be used by the Dalex-related components. This may take a while for larger datasets, so running this once in the notebook will save time, instead of running it every time in the dashboard for each Dalex-related components.
10. After the assignments of the necessary inputs, the dashboard can now be run by feeding the necessay inputs per tab. Click the `http://192.168.100.24:8050` to view the custom dashboard in another tab.

# Installation
## Cloning the Project 
Using Git Bash, type the following in your preferred location of the cloned directory:
```
git clone https://github.com/gaberamolete/XRAIDashboard.git
```
You can also download the zip file of this repository, and extract it in your preferred location.

## Setting up the Environment 
To easily create the environment for XRAI in your local machine, you can run the following in a command prompt or terminal.
```
conda env create -f environment.yml
```
The `environment.yml` is the latest environment with no dependency issues, while the `latest_env.yml` has some due to the addition of the Responsible AI library. Some components in the dashboard may not be available from `environment.yml`.

After creating an environment, you can create a kernel to enable the notebooks to use the conda environment using the following lines.
```
python -m ipykernel install --user --name=XRAI
```

## Requirements
A new folder called "xrai" should be created. download the requirements via `pip3 install -r requirements.txt`. You might need to include `--timeout=1000`.
After installation, download the XRAIDashboard package and input the following in your terminal. 

```bash
cd xrai/dist
pip3 install XRAIDashboard-1.0-py3-none-any.whl
```
If this doesn't work, the package might already be pre-installed. To check, try opening any notebook and do

```bash
import XRAIDashboard
dir(XRAIDashboard)

```

or run "Play with XRAI tool.ipynb" and run the cells that import functions

<!-- The Toolkit currently runs in Python versions 3.7 to 3.9. Please ensure that you have the correct libraries and dependencies installed by checking `requirements.txt`.

Due to some file dependencies, you will need to download these packages separately after installing those in `requirements.txt`:
- Missing `suod` (`PyOD`) - `pip install suod`
- Missing `dtreeviz` - `pip install dtreeviz`
- Missing dependencies of `explainerdashboard` - `pip install explainerdashboard>=0.4.3`
- Missing dash mantine components - `pip install dash_mantine_components`
- Missing Adversarial Robustness Toolbox - `pip install adversarial-robustness-toolbox`
- Missing `raiwidgets` - `pip install raiwidgets>=0.30.0` -- also installs `interpret-community` -->
