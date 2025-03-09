# Market-Basket-Analysis
Project completed in pursuit of Master's of Science in Data Analytics.

## PART I: RESEARCH QUESTION

### PROPOSAL OF QUESTION

What are the most common prescription combinations among patients in the dataset?

### DEFINED GOAL

One goal of Market Basket Analysis (MBA) is to identify which prescriptions patients are more likely to be taking together. Understanding this can assist the hospital in learning more about their patients and may help them in reducing patient readmission rates.

## PART II: MARKET BASKET JUSTIFICATION

### EXPLANATION OF MARKET BASKET

Before one can begin MBA, you must assess whether the dataset has any blank rows and/or columns. If there are any, then remove any row or column that is fully blank. The dataset should be a transactional-type dataset containing typically an ID and the name of the “transaction.” In this example, the IDs are the prescription number and the names are the prescriptions themselves. The dataset must be first transformed into a form suitable to apply apriori. Transform the data by using mlxtend’s Transaction Encoder which converts the dataset into a one-hot encoded numpy array. Then the array is transformed back into a DataFrame where each column will represent the name of the prescription, and each row represents the transaction (Raschka, 2014-2023).

Then the apriori algorithm is applied which finds all combinations of prescriptions in the dataset based on the specified minimum support threshold metric. We can then create a rules table based on what apriori finds, which will allow us to prune the list of rules that can show us the top rules based on specified thresholds such as support, confidence, lift, leverage, conviction, and Zhang’s metric (Selvaraj, 2023).

Personally, I feel that there are overlapping prescriptions in the world that are prescribed to certain patients. For example, an overweight patient may be on high blood pressure medication and may also be on a weight loss medication as well. I am no medical expert, but I believe this analysis will show several medications that are positively paired together given the pruning of the dataset to meet our minimum support thresholds. 

### TRANSACTION EXAMPLE

![IMG_1643](https://github.com/user-attachments/assets/99caea2b-c8e0-4365-a812-0b1dee6716f6)

### MARKET BASKET ASSUMPTION

MBA looks to suggest that if a then b, but for causality to be properly applied, the rest of the data must be controlled. For example, if a patient is prescribed anti-anxiety medication for a temporary period of time, but then years later is prescribed heart medication, you could infer using MBA that the anti-anxiety medication has a high support for the heart medication, when in reality the amount of time between the two prescriptions would not suggest any causality relationship between them. Therefore, one assumption of MBA is that there were no significant changes in the patients during the time in which the data was retrieved (Deniran, 2023).

## PART III: DATA PREPARATION AND ANALYSIS

### CODE EXECUTION

See attached ipynb for all code.

### ASSOCIATION RULES TABLE

Below is a screenshot which shows the top 5 rules based on support, confidence, and lift. 
```python
basket = (rules[['antecedents', 'consequents', 'support', 'confidence', 'lift']])

basket.sort_values(['support', 'confidence', 'lift'], ascending = False).head(5)
```
![IMG_1646](https://github.com/user-attachments/assets/78ca7b00-4f87-48ab-9bda-a1aa564b9c4b)


C4. TOP THREE RULES

The top three rules in this analysis are sorted by those having the highest support metric. The rules table was created by focusing on the support metric with a minimum threshold of 0.01. This produced 432 rules. The top three rules are shown below.

![IMG_1647](https://github.com/user-attachments/assets/df98259a-77c1-4bff-96bb-f2a991ee77a2)

In the top three rules of this analysis, we can see significant contributions for support, confidence, and lift. Observing the first two rules, we can see that they are reciprocal in support and lift. Nearly 6% of all patients are prescribed Carvediol and Abilify together. Also, patients being prescribed Carvediol and Abilify are 1.44 times more likely than chance. Regarding confidence, there’s a 34.3% chance a patient being prescribed Carvediol will also be prescribed Abilify. The opposite of that prescription combination drops down to a 25.1% confidence. Therefore, it is more likely that a patient will first be prescribed Carvediol over Abilify. 

The third rule shows us that for patients being prescribed Diazepam, 5.2% of them are also prescribed Diazepam. These patients taking Diazepam are 1.35 times more likely to be also taking Abilify than not. There is a 32.1% chance that patients prescribed Diazepam will also take Abilify. 

## PART IV: DATA SUMMARY AND IMPLICATIONS

### SIGNIFICANCE OF SUPPORT, LIFT, AND CONFIDENCE SUMMARY

In terms of Market Basket Analysis, Support indicates how frequently an occurrence of a combination of prescriptions appear in the data. It is measured by dividing the number of transactions that contain the items by the total number of transactions. Confidence measures the likelihood of one prescription being prescribed when another one has already been prescribed. And lift compares the observed relationships between prescriptions to what would be expected by chance. 

For this analysis, the top two rules illustrate a significant contribution since we have a support of 5.9% for Carvediol and Abilify as both antecedent and consequent. This is significant since it shows that 6 out of 100 patients in our dataset that are taking these medications together. Measuring the lift, given that our metrics show values larger than 1.0 we can deduce that the antecedents are far more likely to cause the consequents than given simple chance. Again, both Carvediol and Abilify are reciprocal antecedent and consequent using our rules table in our analysis. Patients are much more likely to be taking these medications together than taking them independently of each other; 1.44 times more likely that is. However, given both strong support and strong lift measurements, this model has relatively low confidence intervals. At 34.3% and 25.1% respectively, the probability that patients are taking Carvediol and Abilify together doesn’t give the level of confidence that is typically viewed as a strong factor.

The third rule in our top 3 rules is also significant in that it shows that just over 5% of all patients that are prescribed Abilify are also taking Diazepam, ranking 1.35 times more likely to be taking Abilify as a result of taking Diazepam than by mere chance. However, again, this rule shows a lower confidence level showing that there is just a 32.1% probability that patients taking Diazepam will also be taking Abilify. 

### PRACTICAL SIGNIFICANCE OF FINDINGS

The practical significance of this analysis shows that there’s a strong relationship between patients taking Carvediol, Abilify and Diazepam. Specifically prescribed for patients having high blood pressure, Carvediol, also can be prescribed to treat anxiety. Abilify is an antipsychotic drug prescribed to treat a variety of mental disorders and conditions. Diazepam is used to treat anxiety, muscle spasms, and seizures. 

This implies there is a high correlation between high blood pressure and anxiety. Understanding that these three prescriptions are often used together can help the hospital better treat future patients with similar symptoms or diseases. This will allow them to optimize which medications to prescribe to future patients which is cost-effective to patients. 

### COURSE OF ACTION

I would recommend to this hospital that they put more emphasis on proving the medical correlation between high blood pressure and mental disorders. By identifying that these diseases often occur together, they could begin working on proactive treatment plans to combat patients’ overall health. They could also develop guidelines that would assist them in uncovering earlier diagnoses of the co-occurring diseases which would help them to even strategically intervene early on in the patient’s treatment that would have a positive impact on their overall physical and mental health. 


## PART V: SUPPORTING DOCUMENTATION

### SOURCES FOR THIRD-PARTY CODE

Pandas (2023, June 28). Retrieved September 27, 2023, from https://pandas.pydata.org/docs/reference/index.html.

Waskom, M. (2012-2022). Seaborn Statistical Data Visualization. Retrieved September 27, 2023, from https://seaborn.pydata.org/index.html.

Raschka, S. (2014-2023). MLxtend. Retrieved October 16, 2024, from https://rasbt.github.io/mlxtend/.

Hull, I., Peterson, A., Nehme, A. (n.d.). Market Basket Analysis in Python. Retrieved October 16, 2024, from https://app.datacamp.com/learn/courses/market-basket-analysis-in-python.

### SOURCES 

Bruce, P.A. (2020). Practical statistics for data scientists. 50+ essential concepts using r and python. O’Reilly Media, Incorporated. WGU Library.

Larose, C.D., Larose, D.T. (2019) Data science using Python and R. Chichester, NJ: Wiley Blackwell.

Amruta. (October 14, 2024). Market Basket Analysis: A Comprehensive Guide for Businesses. Retrieved October 16, 2024, from https://www.analyticsvidhya.com/blog/2021/10/a-comprehensive-guide-on-market-basket-analysis/. 

Megaputer. (September 1, 2000). An introduction to market basket analysis. Retrieved on October 16, 2024, from https://www.megaputer.com/introduction-to-market-basket-analysis/.

Selvaraj, N. (April 24, 2023). How to Perform Market Basket Analysis in Python. Retrieved on October 16, 2024, from https://365datascience.com/tutorials/python-tutorials/market-basket-analysis/.

Deniran, O.H. (November 27, 2023). Boosting Sales with Data: The Power of Market Basket Analysis in Retail. Retrieved on October 16, 2024, from https://medium.com/@chemistry8526/boosting-sales-with-data-the-power-of-market-basket-analysis-in-retail-c79cc10a14df.
