---
aliases: []
tags: [microsimulation, multiple_imputation, missing_data, longitudinal]
author: "Spratt M"
URL: "https://pubmed.ncbi.nlm.nih.gov/20616200/"
title: "Spratt 2010 - Strategies for Multiple Imputation in Longitudinal Studies"
type: "literature"
status: "nascent, in-progress, gardening"
year: "2021-11-01"
---

# Key Points

> What are they key takeaways from this literature
-  Complete case generally underestimates prevalence of asthma. Not subtantially but is biased. Bias correction can be done with Multiple Imputation.

-  However this requires inclusion of variables that are associated with both probability of missingness and the outcome variable. Graphs and regression modelling can be used to investigate plausability of these variables and that the MAR assumption holds. If there are no such variables multiple imputation wont do much vs complete case but can still remove some bias. 

-  Generally MI models are more complex than analysis models in order to include these variables. They include as many variables as possible to ensure MAR is satisfied.  However the user should be selective. Variables that are associated to variables with the most missing data are most useful in reducing bias. In this case wheezing at 69 months greatly predicts wheezing at 81 months. Variables that only affect the probability of missingness are not as useful. In this case inclusion of socio-economic variates could've been avoided.

-  Diagnostics of imputed variables should be used. Distributional differences, structural differences should be explained. For example, if analyses exploits the multilevel nature of longitudinal data the imputation should follow this structure. Any differences in distributions I.E. higher mean must be justified. 

- MI can improve efficiency of any associative estimates. This acts as an inflated sample size. 

- Once the MI model and number of imputations is chosen. Variablity between imputed datasets depends on the type of imputation and fraciton of missing data.  Should use at least 25 imputed datasets to reduce variance in association estimates. Low numbers of imputed datasets will struggle due to Monte Carlo randomness. 
  
# Motivation

> Why was this literature written what problem is it addressing?
- Missing data inevitable in longitudinal studies. Complete case analysis is biased outside of MCAR data. Multiple imputation proposed as a solution to these problems.
- There is little guidance on how to publish anlyses from MI particularly for including variables associated with missingness, variables predictive of those variables that are subject to missing data, or both. How many imputed sets to use is also of interest. This paper presents guidance with examples on the ALSPAC longitudinal survey for analysis of asthma. 

# Background

> What previous work has been done towards this problem?
- Not much background in this paper. see motivation. 

# Methods

> What methods were used? How do they address any issues?
- ALSPAC is a prospective study for pregnant women in the UK between 1991-1992. 13988/14541 children born survived their first year. 61% response rate for 81 month study. 
- Outcome of interest was childhood asthma assessed if a child has wheezed within 12 months of being 81 months old. previous at current questionnaires. Considered gender, maternal asthma, smoking variables. Estimated odds ratios using logistic regression from complete cases. 
- Want to determine difference in analyses before and after MI. MI considered further variables not in analysis including 10 binary socio-economic indicators, binary indicators of wheezing between time points at 6,18,30,42,54,69 months were also used.
-  Used logistic regressions to determine which variables predicted missing data (81 month wheeze). Compare MI including variables that predict missingness, variables that predict thiose variables or both using three separate imputation models. first model includes all variables related to outcome/predictor data being missing. Second model included all predictors of wheeze at 81 months. Model 3 included both. All these models fit MI with chained equations (1). An imputed data set uses 10 cycles of this method. 200 imputed datasets are created total. Analyses on each of these are combined using Rubin's rules.  Estimated fraction of missing information was calculated for each model as the ratio of between-imputation variance to the sum of between and within imputation variances. 
	$$\% missing\_information = \frac{between}{between + within}$$
- The whole process is repeated 50 times using 5,10,20,40,200 imputed datasets to account for randomness in MI. 

# Results

> What was the outcome of the research? Was it successful?
- 39.3% had complete data on all variables of interest. Only 2.9% had complete data apart from wheeze at 81. Missingess was usually due to attrition. all genders were recorded, 88% reporeted maternal asthma, 94% reported whether they smoked. 60% had outcome wheezing at 81 observed. 57% had all 3 prognostic variables observed as well. 
- Investigation of which variables predicted missingess was done using complete data to predict binary response or not. Smoking and some socioeconomic variables were associated with wheeze at 81 being missing. Few variables predicted maternal asthma or smoking being missing. Wheeze at 81 was associated with maternal asthma and smoking being missing. 
- Wheeze at 81 weakly assocaited with maternal asthma, weak evidence for gender and maternal smoking too. Association between wheeze at 81 and previous wheezing is strong, particularly for 69 months (OR 11.2, 17.8), This implies accurate prediction of wheeze at 81 for those who are missing data at 81 (n=404). No assocation between socio-ecnomoic variables and wheeze 81. No evidence of association between earlier wheeze and missing data on key variables. Wheeze at 69 was assocatied with missing data at 81 (1.08, 2.06). 
- Prior results outlint assocations between predictors and probility of being missing. They also look at predicting the values of variables that predict missing data. Smoking and maternal were associated with the outcome and it being missing. It is not plausible to assume MCAR. However, the strata formed by these variables, assuming distributions of observed and missing wheeze at 81 are similar can be assumed MAR.  Analyses will be unbiased if both of these variables are included in complete case analysis or imputation. 
![[Screenshot 2021-11-01 at 12.01.46.png]]
- Prevalence of wheeze was assessed using 3 types of imputed and complete case poplulateions defined above. All imputation models included gender, maternal, smoking, and socio-economic (model 1 only), previous wheeze (model 2 only), and both (model 3 only). Assuming MAR holds differences between estimates for complete and imputed data should show bias corrections. 
- Prevalence rises from 13.3-14.1 percent prevalence in model 3 imputed dataset. increases odds ratios for wheeze at 81 with gender, maternal, and smoking by 7, 3, and 6% respectively. Little difference between full and partial imputed models. Distributions for variables were the same between imputed and observed data. 
- Model 2 increased efficiency of analyses with 0.96, 0.94 and 0.85 standard error log odds ratios for gender, maternal, and smoking. This is in theory 10, 12 and 28% increases in sample size. 
- With repeat MI modelling using larger samples the standard error of estimates decreased. As expected more imputed sets lowers standard errors of log odds estimates. 



# Glossary
Any new words should be defined here or reference from the main glossary in /Utility/glossary.  If there isnt a file in the main glossary you can still tag it here and create it later.
1. 

# References
1. Royston P. Multiple imputation of missing values: update.  Stata J. 2005;5(2):188–201.
2. Bodner TE. What improves with increased missing data imputations? Struct Equ Modeling. 2008;15(4):651–75