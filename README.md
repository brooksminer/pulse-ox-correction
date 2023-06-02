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

Our test results show that our classification model is able to accurately predict which individuals are likely to have Hypoxemia despite SpO2 measurements that say otherwise. Our regression model was also able to provide a significantly better estimate of blood oxygenation, performing (...)% better than the current medical standard. 

# Model and Data Details
Our models are built using XGBoost. Our regression model uses builds a gradient boosted forest using the XGBRegressor class, and our classifier builds an ensemble of gradient boosted forests using the XGBClassifier class. 
The data starts with some 
