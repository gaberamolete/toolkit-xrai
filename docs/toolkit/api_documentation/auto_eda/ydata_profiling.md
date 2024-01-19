---
layout: default
title: XRAIDashboard.eda.auto_eda.ydata_profiling_eda2
parent: XRAIDashboard.eda.auto_eda
grand_parent: XRAI API Documentation
has_children: false
nav_order: 2
permalink: /docs/toolkit/api_documentation/auto_eda
---

# XRAIDashboard.eda.auto_eda.ydata_profiling_eda2
**[XRAIDashboard.eda.auto_eda.ydata_profiling_eda2(data)](https://github.com/gaberamolete/XRAIDashboard/blob/main/eda/auto_eda.py)**


Utilizing [Y Data Profiling Package](https://github.com/ydataai/ydata-profiling), previously known as Pandas Profiling, to generate one comprehensive HTML report containing EDA and statistics per features and the data as a whole.


**Parameters:**
- data (pandas.DataFrame) - Data to analyze and extract visualization with.

**Returns:**
- None

*Note: 1 HTML report will be generated in `assets` folder once the function is executed. If you don't have `assets` folder, create one to avoid error for this function*