# Identification of Person-of-Interest in the Enron Scandal

This is a project for the Udacity Introduction to Machine Learning course. It involves using machine learning techniques to identify 
persons of interest in the Enron Scandal, which is a case about corporate fraud. For more information on it, please click [here](https://en.wikipedia.org/wiki/Enron_scandal).

Here is my answers to questions for the project:

1. Summarize for us the goal of this project and how machine learning is useful in trying to accomplish it. As part of your answer, give some background on the dataset and how it can be used to answer the project question. Were there any outliers in the data when you got it, and how did you handle those?  [relevant rubric items: “data exploration”, “outlier investigation”]

The goal of the project is to construct a classifier that can predict whether someone is a person of interest in the Enron corporate fraud. A classifier is an algorithm that has statistically incorporated behaviors from data obtained in the past. In layman's terms, an algorithm is a mathematical formula derived from data already available. It predicts an outcome using the formula from another data set that the formula hasn't encountered before.

For the Enron corporate fraud case, data on various Enron employees' financial information as well as email information with information on who the persons of interest were are available and could be used to statistically come up with a formula or algorithm that could predict persons of interest in the same case. But before an algorithm can be extracted from the data available, the data need to be properly set up and be free from errors that can lead to a misleading algorithm. In the Enron email and financial data set, some items that need to be straightened up were the presence of datapoints (rows in the dataset table) that should not be there, such as "TOTAL" and "THE REGENCY AT THE PARK" which are obviously not persons. The datapoint "TOTAL" was determined by obtaining the scatterplot of features "salary" and "bonus". After the removal of this datapoint, the scatterplot does not show any more outliers.

2. What features did you end up using in your POI identifier, and what selection process did you use to pick them? Did you have to do any scaling? Why or why not? As part of the assignment, you should attempt to engineer your own feature that does not come ready-made in the dataset -- explain what feature you tried to make, and the rationale behind it. (You do not necessarily have to use it in the final analysis, only engineer and test it.) In your feature selection step, if you used an algorithm like a decision tree, please also give the feature importances of the features that you use, and if you used an automated feature selection function like SelectKBest, please report the feature scores and reasons for your choice of parameter values.  [relevant rubric items: “create new features”, “properly scale features”, “intelligently select feature”]

The features I eventually used were the result of plotting histograms for each feature and determining weather there is enough variation (spread) in the data within that feature. It would have been nice if there was total separation in the histograms for the poi (persons-of-interest) and the non-poi, but there really is none. For more information on this, please see the Jupyter notebook for the histograms. 

In class, the calculation of fractions for emails sent to poi and emails obtained from poi was discussed, so it was included in the analysis. After calculating the fractions resulting to new, derived features "fraction_to_poi" and "fraction_from_poi", the raw data used for calculation were then not used in the machine learning for obvious reasons. 

Aside from the reasons I stated above, I have no more reasons to remove any more features, as I planned to use principal component analysis (PCA), which I think is a great dimensionality reduction tool I can use. Out of the possible 22 features from the email and financial dataset, I was left with 16 features, which I subjected to scaling, then dimensionality reduction, and then eventually classification. Scaling for the Enron case is critical as discussed in the class--since the features have varying scales: "fraction_from_poi" and "fraction_to_poi" would have values lower than 1, while "salary", "bonus", etc. are in the millions. Using PCA allowed me to not do any more feature selection algorithm as PCA incorporates information from raw features into new "features" that are going to be eventually used in the classification. After PCA, I don't feel there is a need for another feature selection. The resulting components are already pretty low in variance, not surpassing 0.5 in explained variance ratio, so really the number of final "features" available for the classification step are only two to three, when I varied my starting features. Having this much number of features for classification, I don't think I need to do another feature selection!

3. What algorithm did you end up using? What other one(s) did you try? How did model performance differ between algorithms?  [relevant rubric item: “pick an algorithm”]

I eventually used Decision Trees as classification algorithm after MinMaxScaler for feature scaling and PCA for dimensionality reduction. This classification algorithm gave me the highest precesion and recall. Other classification algorithms have lower or even higher accuracy score, but gave disappointing precision and recall scores. When using Decision Trees, I was able to at least identify Ken Lay and Jeff Skilling as poi (there were 2 true positives!). The Jupyter notebook should show the results I obtained for all classification algorithms I tested. I used the pipeline function to perfom scaling, dimensionality reduction and classification (along with GridSearchCV).

4. What does it mean to tune the parameters of an algorithm, and what can happen if you don’t do this well?  How did you tune the parameters of your particular algorithm? (Some algorithms do not have parameters that you need to tune -- if this is the case for the one you picked, identify and briefly explain how you would have done it for the model that was not your final choice or a different model that does utilize parameter tuning, e.g. a decision tree classifier).  [relevant rubric item: “tune the algorithm”]

Tuning the parameters for the classification involves determining the optimal parameters available for the particular algorithm that results in the highest metric scores. For example in the decision tree classifier I used, one parameter I played around with is min_split.... I was easier to use the GridSearchCV function to determine the optimal parameters. 

5. What is validation, and what’s a classic mistake you can make if you do it wrong? How did you validate your analysis?  [relevant rubric item: “validation strategy”]



6. Give at least 2 evaluation metrics and your average performance for each of them.  Explain an interpretation of your metrics that says something human-understandable about your algorithm’s performance. [relevant rubric item: “usage of evaluation metrics”]



