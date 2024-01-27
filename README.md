# Cell Quality Metric Design and Evaluation - Decision Making

<div align="center">
  <img src="https://github.com/Ting-DS/Cell-Quality-Metric-Design/blob/main/Tesla_logo.png" width="40%">
</div>

## Background 

This task is one of [Tesla Data Engineer](https://www.tesla.com/careers/search/job/data-engineer-208942) & Analyst Take-home Challenges. My solution is not comprehensive and completely correct, but I passed the take-home project interview with it. Now I am sharing the project background and solution for public's reference! Please find the task instruction [here](https://github.com/Ting-DS/Cell-Quality-Metric-Design/blob/main/Instructions.docx)

Imagine that Tesla has ventured out into selling phones. To ensure the highest quality of these phones, the company collects and analyzes corresponding manufacturing data that allows them to further improve existing manufacturing processes. A part of the production line are three zones of quality inspection for phone parts. After all inspections are done, finished phones are randomly classified into different groups for shipment across identified markets. Your manager has approached you to give a report on which group of phones are of the highest quality based on the manufacturing data given below. 

According to the results of three quality inspection areas for phone components, select the highest quality phone and provide an explanation.

## Manufacturing data
 - phoneID: unique identifier of product
 - criteria A/B/C: number of parts that passed a certain criteria inspection (i.e., functioning LED screen)
 - TotalPartsInspected: total number of parts that underwent all three inspection zones
 - classification: product classification/group (letter classifications are not ordered in any way)

Note: All parts undergo inspection in all three zones. However, different phone variants (pro vs regular versions) will have varying number of parts inspected.

## Questions




