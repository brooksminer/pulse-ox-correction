# Correcting Racial Bias in Pulse Oximeter Measurements of Blood Oxygen Saturation
Erdős Institute Data Science Boot Camp Spring 2023

**Awarded 1st place among 33 projects by a panel of data science professionals**

Team Members:
- [Brooks Miner](https://www.linkedin.com/in/brooks-miner/)
- [Jaychandran Padayasi](https://www.linkedin.com/in/jaychandran-padayasi/)
- [Rohan Myers](https://www.linkedin.com/in/rohanmyers/)
- [Saad Khalid](https://www.linkedin.com/in/saad-khalid-9b31b3125/)
- [Woojeong Kim](https://math.indiana.edu/about/graduate-students/Kim-Woojeong.html)

# Project Description

Inequity in the quality of healthcare based on your social identity, such as your race or gender, is a long-standing issue in medicine. While this issue is recently starting to receive some well deserved attention, there is still a long way to go. One manifestation of this problem is the innacuracies in blood oxygen measurements in people of color when using a pulse oxymeter. As stated by the PhysioNet team[[1]](https://physionet.org/content/mit-critical-datathon-2023/1.0.0/):

>Pulse oximeters are medical devices used to assess peripheral arterial oxygen saturation $(SpO2)$ noninvasively. In contrast, the "gold standard" requires arterial blood to be drawn to measure the arterial oxygen saturation $(SaO2)$. Pulse oximetry inaccuracies can fail to detect episodes of hidden hypoxemia, i.e., low SaO2 with high SpO2. Hidden hypoxemias can result in less treatment and increased mortality. Yet flawed, pulse oximeters remain ubiquitously used because of their ease of use; debiasing the underlying algorithms could alleviate the downstream repercussions of hidden hypoxemia.<br>

We tackle this problem by developing two models, one to predict $SaO2$ and one to predict Hidden Hypoxemia, using features that do not require a blood draw. Our model is trained on a publicly available dataset of de-identified medical records from 50,000 unique patients at Beth Israel Deaconess Medical Center in Boston, MA, between 2008 - 2019.<br>

Our test results show that our classification model is able to accurately predict which individuals are likely to have Hypoxemia despite SpO2 measurements that say otherwise. Our regression model was also able to provide a significantly better estimate of blood oxygenation, outperforming the current medical standard by 30% for patients with hypoxemia.<br>

# Evidence of Racial Bias
From our data, we can see that rates of Hidden Hypoxemia are higher for people of color.
![image](https://github.com/brooksminer/pulse-ox-correction/assets/12636792/07c8aba1-953b-4dc2-8baa-98aa485cb1ba)

# Model and Data Details
Our models are built using XGBoost. The data starts with some erroneous SpO2 and SaO2, and some of the features have NaN entries. We clean our data by removing the erroneous data and using Scikit-Learns IterativeImputer to impute the NaN entries. <br>

For the SaO2 Regression Model, we logit-transformed SpO2 and SaO2 values to normalize values for a better regression fit. The dataset has a highly skewed distribution with most SaO2 and SpO2 values lying close to the upper measurement boundary of 100, making naïve regression ineffective. Our model provides estimates that are 30% closer to the actual blood oxygenation for patients with hypoxemia than the current medical standard of only using pulse oximetry measures. <br>

Hidden hypoxemia is a rare event, accounting for only 1.6% of the patients in our dataset. Building a classifier that accurately finds these patients without overestimating their prevalence is difficult. For the HH Classification Model, we used an ensemble of gradient boosted forest classifiers created using XGBoost. The ensemble is trained on random undersamplings of the dataset in order to counter the imbalance in classes and artificially boost the prevalence of hidden hypoxemia in training.

Pipeline for the Classification Model:<br>

![image](https://github.com/brooksminer/pulse-ox-correction/assets/12636792/23613069-9ae7-4752-a936-fc221c36c84a)



# Dependencies
Running the code requires the following Python packages: 
```
XGBoost, Scikit-Learn, Pandas, Numpy, Matplotlib
```
# Interfacing with Models and Data Analyses
Exploratory data analysis is located in EDA folder, in the `EDA_Oximetry_Data_MIMIC-IV.ipynb` notebook. The notebook for creating the classifier can be found under Notebooks in `Classifier_Undersampling.ipynb`. The Regression Model can be generated using the `SaO2_Regression_Model.ipynb` file under the Notebooks folder. 

# Data Usage
The data is publically available through [PhysioNet](https://physionet.org/content/mit-critical-datathon-2023/1.0.0/). Accessing the data requires completing the CITI Data training, information for which can be found at the bottom of the linked page. 

# Applying the Classifier
We've deployed a [web app](https://huggingface.co/spaces/zonova/pulse_ox) showcasing a minimal feature version of our model. 
Here is an example run:
![image](https://github.com/brooksminer/pulse-ox-correction/assets/12636792/6d3e09bb-4778-4b4d-aa76-dfb59e185eb4)

