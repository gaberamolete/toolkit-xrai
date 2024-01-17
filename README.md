# Explainable and Responsible AI Toolkit
***Developed by AI&I COE***

The **DSAI Explainable and Responsible AI (XRAI) Toolkit** is a complementary tool to the [XRAI Guidelines document](https://unionbankphilippines.sharepoint.com/:b:/s/DataScienceInsightsTeam/EbGWZEJkn7REt1zzHspu-xABsLDpD1eD6mgHMjPJypnzdA?e=wm55U7). The Toolkit provides a one-stop tool for technical tests were identified by packaging widely used open-source libraries into a single platform, according to ADI/DSAI user needs. These tools include Python libraries such as `shap`, `dalex`, `dice-ml`, `alibi`, `netcal`, `aif360`, `scikit-learn`, and UI visualization libraries such as `raiwidgets` and `plotly`. This toolkit aims to: 
- Provide a user interface to guide users step-by-step in the testing process; 
- Support certain binary classification and regression models that use tabular data 
- Produce a basic summary report to help DSAI System Developers and Owners interpret test results 
- Intended to be deployable in the user’s environment

Subsequent versions and updates will be found in the XRAI [GitHub repo](https://github.com/aboitiz-data-innovation/XRAI), accompanied by XRAI Brownbag sessions.

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