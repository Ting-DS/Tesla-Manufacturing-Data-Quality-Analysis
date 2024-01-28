# Tesla Phone Quality and Reliability Evaluation

<div align="center">
  <img src="https://github.com/Ting-DS/Cell-Quality-Metric-Design/blob/main/Tesla_logo.png" width="20%">
</div>

## Background 

This task is one of [Tesla Data Engineer](https://www.tesla.com/careers/search/job/data-engineer-208942) & Analyst Take-home Challenges. My solution is not comprehensive and completely correct, but I passed the take-home project interview with it. Now I am sharing the project background and solution for public's reference! Please find the task instruction [here](https://github.com/Ting-DS/Cell-Quality-Metric-Design/blob/main/Instructions.docx)

Imagine that Tesla has ventured out into selling phones. To ensure the highest quality of these phones, the company collects and analyzes corresponding manufacturing data that allows them to further improve existing manufacturing processes. A part of the production line are three zones of quality inspection for phone parts. After all inspections are done, finished phones are randomly classified into different groups for shipment across identified markets. Your manager has approached you to give a report on which group of phones are of the highest quality based on the manufacturing data given below. 

According to the results of three quality inspection areas for phone components, select the highest quality phone and provide an explanation.

## Manufacturing data
 - phoneID: unique identifier of product
 - criteria A/B/C: number of parts that passed a certain criteria inspection (i.e., functioning LED screen)
 - TotalPartsInspected: total number of parts that underwent all three inspection zones
 - classification (A/B/C/D/E): product classification/group (letter classifications are not ordered in any way)

Note: All parts undergo inspection in all three zones. However, different phone variants (pro vs regular versions) will have varying number of parts inspected.

## Questions

#### 1. Define key quantitative metrics to compare different phone groups and provide reasons specifically
#### 2. Determine which phone group has the highest quality and provide recommendation supported by data visualization and narratives.
#### 3. Specify all assumptions while answering the above two questions

## Analysis
#### 1. Data structure & Data preprocessing & Sanity Check
 <div align="center">
  <img src="https://github.com/Ting-DS/Cell-Quality-Metric-Design/blob/main/png/data structure.png" width="60%">
 </div>
 
 For each phone group (A/B/C/D/E) seperately:
 - Check total number of parts inspected, to see if there is an imbalance: 
 - Check the distribution of number of parts that passed each criteria (A/B/C) and total number of parts inspected

#### 2. Metric Design & ANOVA test

Since total number of parts inspected is similar among different phone groups, therefore we can use the pass ratio/proportion to compare different phone groups, making it easier to identify patterns or differences.

Since all parts undergo inspection in all three criteria, which means the part that undergo all three criteria are the same. Therefore, there is no bias towards specific criteria when we calculate the overall pass ratio by averaging the 3 pass ratios of each criterion.

For each phone group (A/B/C/D/E) seperately:
   - [Average pass ratios of each criteria] = (# of passed parts of each criteria) / (total # of parts inspected) : 3 ratios for each criteria (A/B/C)
   - [Overall criteria pass ratios] = AVG pass rates of all 3 criteria

 <div align="center">
  <img src="https://github.com/Ting-DS/Tesla-Phone-Quality-Evaluation-Decision-Making/blob/main/png/mean.png" width="90%">
 </div>

The one-way ANOVA test shows that there is no significant difference of each metric among different phone groups.

#### 3. Metric Distribution
 <div align="center">
  <img src="https://github.com/Ting-DS/Tesla-Phone-Quality-Evaluation-Decision-Making/blob/main/png/distribution.png" width="90%">
 </div>
The distribution of each metric is approximately normal distribution, except for criteria B pass ratio is a little left-skewed.

Therefore, we can estomates 95% confidence interval of the distribution of pass ratio of three criteria and overall criteria, to evaluate the variability of each metric.
The following displays the results of overall pass ratios.

 <div align="center">
  <img src="https://github.com/Ting-DS/Tesla-Phone-Quality-Evaluation-Decision-Making/blob/main/png/overall%20ratio.png" width="40%">
 </div>

#### 4. Modeling (OLS linear regression)

Create four OLS linear regression models with the same independent variables: a categorical variable (phone group) and the total number of inspected parts. The outcomes should be 'criteriaA_pass_through_rate', 'criteriaB_pass_through_rate', 'criteriaC_pass_through_rate', and 'criteria_overall_pass_through_rate' respectively.

Observe the contribution and significance of different phone groups to four outcomes. The following displays the results of overall pass ratios.

 <div align="center">
  <img src="https://github.com/Ting-DS/Tesla-Phone-Quality-Evaluation-Decision-Making/blob/main/png/OLS.png" width="50%">
 </div>

## Conclusion

Comparably, the classification phone group E has a slightly higher quality, because The ANOVA test shows that there is no significant difference of each metric among different phone groups:
 - The classification E has a relatively higher **average** pass rate for criteria A, B and overall, only a slightly lower pass rate than other classes using criteria C.
 - Based on the 95% confidence interval, the pass rates for all classifications are similar in range, indicating **comparable variability**.
 - Using the `classification` and `TotalPartsInspected` to regress on different metrics, the summary table align on the same conclusion: while other conditions are the same, the classification E has a relatively higher performance than other classes (the classification E has highest positive coefficients value and T-statistics in criteria A, B and overall metrics modeling)

## Acknowledgement

Thanks to [Tesla](https://www.tesla.com) for providing this data analysis challenge dataset and questions, which allows to define, analyze and evaluate metrics from different perspectives, broadening the vision of data analysis and statistical modeling.









