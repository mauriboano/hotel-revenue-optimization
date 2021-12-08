# Hotel Revenue Optimization

### This repository contains the code used for the final group project of my DS5559 Big Data Analytics class while at the University of Virginia's MS in Data Science program. Below you will find the abstract written for this work and a focus on the business logic implemented for the `net_rev` function.

## Abstract
Though some booking industries may be permitted to overbook, hotels are legally required to have space for all customers with a reservation. This analysis focuses on the hotel industry and whether cancellations can be predicted with the goal of contacting the customer and rebooking their room to recover potentially lost revenue.

The analysis makes use of a dataset available on kaggle.com which has a binary response variable indicating whether a reservation was canceled, in addition to a multitude of categorical and numerical explanatory variables. Several packages within PySpark’s ML library are leveraged in order to model predictions, as well as for performing exploratory analysis and requisite preprocessing tasks. Business logic is then applied in order to both optimize threshold boundaries and estimate the net revenue gained for evaluating performance.

Our findings indicate that all models tested would lead to an increase in net revenue, but that a random forest model leads to the highest net revenue gain--generating close to $680K in additional revenue based on a validation set representing a period of over 5 months.

## `net_rev` Function
In the code, AUPRC is used as the cross-validation metric. However, it is not the best solution for optimizing the threshold or for estimating the business impact of any of these models. For this, we developed a net revenue function that takes as input:

* Probabilities or rawPrediction values associated with a cancelation
* A single value or list of values to be tested as the threshold parameter
* A multitude of values representing business assumptions

With this information, this function estimates the net revenue generated by the model probabilities and threshold provided.

![code_snip](https://user-images.githubusercontent.com/1994967/145266921-812bf543-9596-4442-8d78-f0e94a08a343.png)

In the event that multiple thresholds are fed into the function, a chart plotting threshold vs net revenue is also provided.

![rf_plot](https://user-images.githubusercontent.com/1994967/145266951-2c0a1615-ccc0-4bac-89c8-bac1c6e5882d.png)

The thought behind implementing this sort of custom evaluation function is that the business value of a true positive and a false positive classification are not equal, so metrics like precision and recall would be insufficient in providing a picture of performance. The figure below visualizes the logic used for estimating the revenue gained by contacting a predicted true positive, and revenue lost by contacting a predicted false positive (information that is of course unknown at the time of prediction). Please keep in mind that all assumptions can and should continue to be tested as more information is available to the analyst.

![flowchart](https://user-images.githubusercontent.com/1994967/145266979-66ebfe7a-1b22-45d6-b455-e1eac2d9f7b2.png)

## Original Project Team (University of Virginia MSDS)
* Aaron Olvier (ao9au@virginia.edu)
* Anvar Sabarnov (as5da@virginia.edu)
* Maurizio Boano (mb6fs@virginia.edu)
* Monish Dadlani (mkd7q@virginia.edu)

