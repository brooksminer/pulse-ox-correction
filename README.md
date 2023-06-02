# Correcting Bias in Pulse Oximeter Measurements of Blood Oxygen 
Erdős Institute Data Science Boot Camp Spring 2023

Team Members:
- Brooks Miner
- Jaychandran Padayasi
- Rohan Myers
- Saad Khalid
- Woojeong Kim

#Project Description
Inequity in the quality of healthcare based on your social identity, such as your race or gender, is a long-standing issue in medicine. While this issue is recently starting to receive some well deserved attention, there is still a long way to go. One manifestation of this problem is the innacuracies in blood oxygen measurements in people of color when using a pulse oxymeter. As stated by the PhysioNet team at MIT[[1]](https://physionet.org/content/mit-critical-datathon-2023/1.0.0/):

>Pulse oximeters are medical devices used to assess peripheral arterial oxygen saturation $(SpO2)$ noninvasively. In contrast, the "gold standard" requires arterial blood to be drawn to measure the arterial oxygen saturation $(SaO2)$. Pulse oximetry inaccuracies can fail to detect episodes of hidden hypoxemia, i.e., low SaO2 with high SpO2. Hidden hypoxemias can result in less treatment and increased mortality. Yet flawed, pulse oximeters remain ubiquitously used because of their ease of use; debiasing the underlying algorithms could alleviate the downstream repercussions of hidden hypoxemia.

We tackle this problem by developing two models, one to predict $SaO2$ and one to predict Hidden Hypoxemia, using features that do not require a blood draw. Our model is trained on a publicly available dataset of de-identified medical records from 50,000 unique patients at Beth Israel Deaconess Medical Center in Boston, MA, between 2008 - 2019.

Our test results show that our classification model is able to accurately predict which individuals are likely to have Hypoxemia despite SpO2 measurements that say otherwise. Our regression model was also able to provide a significantly better estimate of blood oxygenation, providing estimates that are closer to the actual blood oxygenation than the current medical standard. 

# Evidence of Racial Bias
From our data, we can see that rates of Hidden Hypoxemia are higher for people who are not White. 

# Model and Data Details
Our models are built using XGBoost. Our regression model builds a gradient boosted forest using the XGBRegressor class, and our classifier builds an ensemble of gradient boosted forests using the XGBClassifier class. 
The data starts with some erroneous SpO2 and SaO2, and some of the features have NaN entries. We clean our data by removing the erroneous data and using Scikit-Learns IterativeImputer to impute the NaN entries. 

# Dependencies
Running the code requires the following Python packages: XGBoost, Scikit-Learn, Pandas, Numpy, Matplotlib

# Interfacing with Models and Data Analysis

# Data Usage
The data is publically available through [PhysioNet](https://physionet.org/content/mit-critical-datathon-2023/1.0.0/). Accessing the data requires completing the CITI Data training, information for which can be found at the bottom of the linked page. 

# Applying the Classifier
We've deployed a [web app](https://huggingface.co/spaces/zonova/pulse_ox) showcasing a minimal feature version of our model. 
Here is an example run:
![image](https://github.com/brooksminer/pulse-ox-correction/assets/12636792/6d3e09bb-4778-4b4d-aa76-dfb59e185eb4)

