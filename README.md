# CoverMyMeds
This Github repository presents a company-sponsored project, with data provided by [CoverMyMeds]( https://www.covermymeds.com/main/). Also, this project is part of the requirements needed for the satisfactory completion of the Data Science Bootcamp offered by the [Erdos Institute]( https://www.erdosinstitute.org/). 

## Team Jaguar members:
* [Shreejit Bandyopadhyayay](https://github.com/Erdos-CMM/CoverMyMeds/tree/shreejit)
* [Craig Franze](https://github.com/Erdos-CMM/CoverMyMeds/tree/franze)
* [Maimaiti Wulayimu (Ibrahim Memet)](https://github.com/Erdos-CMM/CoverMyMeds/tree/ibrahim)
* [Emily Phillips-Longley](https://github.com/Erdos-CMM/CoverMyMeds/tree/ellongley)
* [Miriam Sierra](https://github.com/Erdos-CMM/CoverMyMeds/tree/miriam)

## Motivation
When a doctor prescribes a therapy to a patient, they send the prescription to a pharmacy. Patients filling their prescription at a pharmacy require an insurance check to ensure their therapy is covered by their insurance. Payers may not cover medications or dosages and may reject the claim. If a claim is rejected, a prior authorization (PA) can be started to prevent prescription abandonment and ensure a patient gets the therapy their provider thinks would work best for them. 

## Proposed Solution 
A classification algorithm tool can tackle these challenges by:
1. Predicting patient pharmacy claim success. We built a classifier designed to predict claim success to inform patients if their insurance will likely cover their therapy.
2. Predicting patient electronic PA (ePA) success. Create a classifier designed to predict ePA success can prevent patients from waiting on a payer’s decision, only to switch to a different medication.  

## The process
### Exploratory Data Analysis
General trends: 
* Drug C had slightly higher claim approval rate, drug B has the lowest. 
* Bin 999001 has the highest claim approval Rate, 417380 and 417614 had the lowest. [See more here](https://github.com/Erdos-CMM/CoverMyMeds/blob/main/Data%20Visualization%20%26%20Trends/Data_Visualization.ipynb)
* Reject code 75 more likely to have their ePA approved, and reject code 70 least likely. [See more here](https://github.com/Erdos-CMM/CoverMyMeds/blob/main/Data%20Visualization%20%26%20Trends/Data_Trends.ipynb)

### Feature Selection Methodology
With general insights into the features relevant to our Classification problem, we sought to formalize the important features for each task.  
* Feature selection methods: 
  * Fit DecisionTree Classifier to assess feature “importance scores” for [Pharmacy Claims](https://github.com/Erdos-CMM/CoverMyMeds/blob/miriam/feature_selection/Feature%20selection%20Claims.ipynb) and [ePA](https://github.com/Erdos-CMM/CoverMyMeds/blob/miriam/feature_selection/Feature%20selection%20PAs.ipynb). 
  * Correlation plot of features with target variable 
  * Train and test model adding features in succession to test for improvement. [See more here](https://github.com/Erdos-CMM/CoverMyMeds/blob/ellongley/notebooks/feature_selection/Feature%20Selection%20-%20ePA%20Prediction.ipynb)

* Feature Selection Results
  1. Relevant features for Claim success predictor: 
      * Bin
      * Drug Type 
  2. Relevant features for ePA success predictor:
      * Reject Code
      * Contraindication
      * Drug Type

### Metric selection rationale
*Classifier #1 Claim Success Predictor*
The goal of this classifier is to predict whether a claim will be successful.  If the classifier predicts that a claim will be successful but the claim is in fact rejected, a patient will have gone to the pharmacy just to leave empty handed, likewise, if the model predicts the claim will not be successful, a patient will have spent time negotiating a different medication with a doctor unnecessarily. 
* We choose Precision as the most important metric. 

*CLassifier #2 ePA Success Predictor*
The goal of this classifier is to predict whether an ePA will be successful.  If the classifier predicts that the ePa will be successful but the payer will in fact reject the case, then a patient will have waited on a decision when they could have been spending time figuring out a different route with their provider. 
* We choose Recall as the most important metric.

### Model Selection
For each problem statement we tested different machine-learning classifiers and recorded the metric performance, keeping in mind their generalization to random selections of the training data. 
* [Logistic Regression](https://github.com/Erdos-CMM/CoverMyMeds/blob/shreejit/Logistic.ipynb)
* [K-nearest neighbors](https://github.com/Erdos-CMM/CoverMyMeds/blob/shreejit/KNN.ipynb)
* [Random Forest](https://github.com/Erdos-CMM/CoverMyMeds/blob/shreejit/Random_forest.ipynb)
* Stochastic Gradient Descent for [Claims](https://github.com/Erdos-CMM/CoverMyMeds/blob/miriam/Classification%20Methods%20Exploration/SGD-Classifier%20for%20Claims.ipynb) and [ePA](https://github.com/Erdos-CMM/CoverMyMeds/blob/miriam/Classification%20Methods%20Exploration/SGD-Classifier%20for%20PAs_1.ipynb)
* Naive Bayes
* [XGBoost](https://github.com/Erdos-CMM/CoverMyMeds/blob/shreejit/Hyperparameter_Tuning_for_XGBoost_for_claims_with_CV.ipynb) 
* [ADABoost](https://github.com/Erdos-CMM/CoverMyMeds/blob/miriam/Classification%20Methods%20Exploration/Tuning%20Adaboost%20with%20Decision%20Tree.ipynb)

## Results 
* For Classifier #1 (claims approval) tuning of hyperparameters of XGBoost gave us the the best metrics.
* For Classifier #2 (ePA) we tuned the hyperparameters of ADABoost, the best performing model in this case. Number of estimators, learning rate and algorithm were the most important parameters checked.

## Conclusions
Providing solutions to ease the path for patients from provider to care is a difficult task. CoverMyMeds’ is providing a means of improving this process by making the journey easier for patients, providers, payers and pharmacies.
* If we assume all claims were successful, ~ 40% of patients will go to a pharmacy for their medication, but not be able to receive it.
* Our models provide precise predictions of patient’s claims success (90%), allowing patients to identify a claim that will not be able to be fulfilled.
* Additionally, our models identify with high success an ePA that will help to ensure a patient receives the medication they need (93.2%). 

## Acknowledgements
We thank the [Erdos Institute]( https://www.erdosinstitute.org/) and [CoverMyMeds]( https://www.covermymeds.com/main/) for all their support in the realization of the project. 

-----
More information about this project can be found in [Executive Summary](https://docs.google.com/document/d/1FwrmBEhBAQWARjeUt4RZFoarkcXRJpPkcrNds7StoyU/edit) and [Video presentation](https://drive.google.com/file/d/1v1xNRlQtk9EyGTjWGuJ4GD-V1L0_eG3i/view?usp=sharing).

 















