# Bank Churn Study

![Imgur](https://i.imgur.com/1l4jsdg.jpg)

## Introduction  

The purpose of this case study is to determine which customers of a bank are most likely to churn, given a static snapshot of the customer pool at a given point in time. If we can identify certain characteristics that are risk factors for churn, we can recommend strategies to increase customer retention.  
  
## The Data  
  
The data comes from [Kaggle](https://www.kaggle.com/sonalidasgupta95/churn-prediction-of-bank-customers). It represents a snapshot of 10,000 bank customers in France, Germany, and Spain. Each observation represents a single customer.  

**COLUMNS:**

**CustomerId:** Unique numeric identifier of customer  
**Surname:** Surname of customer  
**CreditScore:** Credit score of customer  
**Geography:** Customer's country of residency  
**Gender:** Male or Female  
**Age:** Age of the customer  
**Tenure:** Number of years the customer has been with the bank  
**Balance:** Bank balance of the customer  
**NumOfProducts:** Number of bank products the customer is utilising  
**HasCrCard:** Binary Flag for whether the customer holds a credit card with the bank or not  
**IsActiveMember:** Binary Flag for whether the customer is an active member with the bank or not  
**EstimatedSalary:** Estimated salary of the customer in Dollars  
**Exited:** Binary flag 1 if the customer closed account with bank and 0 if the customer is retained  
  
## Methodology  

Since the data set includes customers who have churned, the objective is to determine whether there are commonalities that are  relatively unique to the set of exited customers (i.e. factors that are shared by exited customers, but not by existing customers). The test would entail running new customers through the algorithm to classify each as "churn" or "stay." By adjusting the classification threshold, we can determine which customers we want to target for retention measures.  
  
I ran the data through six different classification algorithms to see which performed best. The two optimal ones were XGBoost and Logistic Regression.  

![Imgur](https://i.imgur.com/KPMw6qv.png)  
  
I tuned and cross-validated the XGBoost model and then honed in on an optimal decision threshold. Recall is more important to our business case, since exited customers are very valuable to us (91,000 euros on average), so I set the F-beta to 1.5. That proved to be a little too insensitive to precision, so I decided on a final threshold of 27%, which yielded a recall of 70%. In other words, if a customer is determined by this algorithm to have a 27% chance or greater of leaving the bank, they should be flagged for interventional measures, and by setting the threshold at 27%, we can expect to successfully identify 70% of all of the people who will actually leave the bank barring intervention.   
  
![Imgur](https://i.imgur.com/oPbWkuL.png)
  
## Findings  
  
Since logistic regression performed nearly as well as XGBoost, it's not unreasonable to rely on its well-known and valuable feature importances attribute. 

![Imgur](https://i.imgur.com/S7PkFRy.png)  

Without more information regarding what the various product offerings are, it's not possible to make product recommendations. However, we can see clearly that the most significant negative predictor of churn is age, and the second-most significant is that the customer is German. The age discrepancy is striking when you plot the age distribution of each customer class: exited and retained.  

![Imgur](https://i.imgur.com/Q4HPdfR.png)

We can see that as customers advance in age, they become much more likely to leave the bank. This presents us with several challenges:
* Older people = more money (mean balance of exited customers = €91,000)
* Wealthier people are less likely to be incentivized by short-term or one-time offers
* It appears that their having more products does not translate to customer retention
  
## Recommendations  
  
A caveat that we should point out is that, to someone from the U.S., it may be tempting to assume that a primary investment consideration for a person entering their 40s might be college education saving for children, however, we must remember that higher education in these countries is much more affordable because there is an abundance of publicly funded options. Therefore, it's reasonable to assume that college savings don’t make up as much of a person’s invested capital. As such, the bank should probably focus on other products, such as retirement products.

* Review competitiveness of rates and robustness of product offerings, especially for retirement products  
* Offer reduced fees to customers 40 and over, perhaps on a sliding scale  
* Investigate why customers with three products are so inclined to exit



