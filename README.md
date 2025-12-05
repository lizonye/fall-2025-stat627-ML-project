# Research Topic: Predicting Deficits in Action Prediction from Tumor Location
## Requirement: Fall 2025, Stat 627, Statistical Machine Learning; American University
### Team: Sally Henley, Ogechi Onyewu, Rebecca Tegiacchi

### Questions of Interest:
1. Can we predict performance accuracy on an action prediction task based on lesion location within the brain (infratentorial vs supratentorial)? 
2. Does age at diagnosis predict performance on the action prediction task or general cognitive performance? 

### Planned Approach:
The cerebellum is a key developmental structure that has been shown to be highly involved in both motor and cognitive functioning. Despite only being 10% of the volume of the brain, the cerebellum contains over half of the brain’s neurons. 

### Literature Review: 
Additionally, the cerebellum has been divided into functional subregions, such that areas associated with motor coordination are located medially, in the vermis, while areas that support cognitive functioning are typically located laterally (Stoodley et al., 2016). Importantly, the cerebellum has been shown to be functionally connected to key cortical areas, such as prefrontal, temporal, and parietal association areas, which are known for functions such as planning, decision making, and language, among others (Stoodley & Schmahmann, 2010). Disruption to cerebellar subregions can be detrimental to cognitive and motor functioning, whether due to tumor, stroke, or atrophy. The universal cerebellar transform theory has been proposed, stating that the cerebellum uses prediction and error signaling from inputs using the cerebro-cerebellar loops, integrating this information and generating internal models that are used to predict actions in multiple domains, including language, affect, and action processing (Leggio & Molinari, 2015; Argyropoulos, 2016).
The cerebellum is extremely important in development. Cerebellar volume peaks between 12-16 years old, which is much later than the timeline of peak cerebrum development (Tiemeier et al., 2010). Unlike the rest of the brain, where early damage typically leads to better outcomes, it is hypothesized that damage to the cerebellum at an early age actually leads to worse long-term outcomes (Scott et al., 2001; Starowicz-Filip et al., 2017). The cerebro-cerebellar circuits are necessary for learning and skill development, as well as encoding the internal models that are necessary for the control of movement and mental representations (Ito, 2008; Stoodley & Limperopoulos, 2016). 

Machine learning is not a new method in neuroscience research. Glaser et al. (2019) discusses the various uses of machine learning, highlighting the prediction of continuous and categorical output using regression and classification. Because the variables used in clinical research are usually not completely separate and distinct, machine learning methods determine if variables can predict each other, especially when the variables aren’t necessarily linear. The various regression methods that will be used in this project have been used extensively in clinical neuroscience research (see Xie et al., 2016; Hoffman et al., 2015; Ritsner & Strous, 2010 for example).

### Data Assessment: 
The data for the current project is from a study conducted by Butti et al. (2020), in which researchers were analyzing the impact of lesion location on predictive accuracy, specifically taking age at diagnosis into account. In this study, participants were shown videos that showed a child performing a task in which they were reaching to grasp an object. Then, they were presented with shortened versions of the same videos and had to predict or infer the outcome. They had results from N = 63 patients. To analyze the impact of lesion location, they split patients into control, supratentorial lesions, and infratentorial lesions, with N = 21 patients in each group. The supratentorial lesions are defined as being outside of the cerebellum, typically in the cortex, while infratentorial lesions are within the cerebellum. For the current analysis, we will use Accuracy Testing as the primary response variable, with predictors including lesion location, age at diagnosis, time since diagnosis, tumor type, FISQ (measure of general cognitive ability), and Social Perception scores. We will treat radiation, chemotherapy, and neurosurgery as covariates. We will also look at the relationship between lesion location on the beta index, which is a measure of the strength of the contextual priors (the degree to which expectations from prior observations of a specific event predict future events). 

### Dataset Overview: 
Dataset Source: Cerebellar Damage Affects Contextual Priors for Action Prediction in Patients with Childhood Brain Tumor

Number of Observations = 63 total 
•	42 combined observations:
o	21 for Supratentorial and
o	21 for Infratentorial
•	21 for Control Group

Response Variables:
1)	Beta Index: Measurement of Response Bias (how likely to make the same association per the probability of occurrence) 

Predictors: 
1)	Tumor type
2)	Tumor location (supratentorial vs infratentorial)
3)	Age at diagnosis (months)
4)	Time since diagnosis (months)
5)	Presence of radiotherapy, chemotherapy, or neurosurgery (covariates)
6)	FSIQ (measure of general cognitive capacity)
7)	Social Perception Scores
8)	Accuracy Testing phase percentages: Associations between contextual clues and actions (preestablished probability of co-occurrence)

### Planned SML methods: 
For Data cleaning and formatting, we remove empty rows, removed duplicate data, merge data, and format as csv.  We normalize features as scaling is important and will be needed for KNN analysis. The project team identified Statistical Machine Learning methods which will be utilized and leveraged to gain data-driven insight to answer proposed questions. Below are the proposed methods and logic overview based on IDA/EDA of the data set.  
Logistic/Linear Regression: Generate generalize model; We already suspect collinearity between clinical information for presence of radiotherapy, chemotherapy, and neurosurgery and tumor type and to address this, we will analyze the VIF and generate covariance matrices and heatmaps to detect and determine which predictors are most correlated.

### Summary:
We will use data collected by Butti et al. (2020) to examine the differences in performance on action prediction tasks based on lesion location within the brain. We will use methods such as linear and logistic regression, Ridge/LASSO regression, KNN, jackknife, and PCR and PLS while using cross validation techniques to assess flexibility and find the best set of predictors. We will compile our models to come up with a final model that creates the best representation of the data. We will use the results from our models to assess the impact of lesion location on task performance and discuss future research that could be conducted to continue to make advances in the field. 

KNN: We will leverage KNN to explore non-linear relationships between features and target variables, which logistic regression may not capture effectively. Compare KNN with logistic regression and PLS for interpretability. Compare MSE with tuned Ridge/LASSO MSE.

Jackknife: We will use this resampling method to estimate stability and variance/bias for the KNN model and for further model evaluation/validation.

Principal Component Analysis [PCA]: Leverage for dimensionality reduction; transform the initial set of predictors with identified multicollinearity to a smaller set of uncorrelated variables called principal components. These principal components will feed the PCR method. We will test implementing PCA before KNN if we have high collinearity between predictors to reduce correlated features and noise.

K-Fold Cross Validation: We will perform this method to analyze cross-validation loops for stacking (stacked model that combines KNN and Ridge/LASSO components) and collect MSE on each fold. We will test k = 5 and k = 10.

Ridge/LASSO: We will use Ridge to handle multicollinearity and LASSO to perform feature selection. Use PCA reduced features and KNN predictions as input.

Principal Component Regression [PCR]: We will use this method to find new features or add new variables.

Partial Least Squares [PLS]: We will use this method after PCR, since PLS considers the response variable(s) during component extraction and maximizes covariance between predictors and response variable(s), which may lead to a better predictive performance than PCR.


