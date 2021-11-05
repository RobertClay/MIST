---
aliases: []
tags: [microsimulation, regression, OLS, random_effects, fixed_effects, GMM, system_GMM]
author: "McLay J"
URL: "https://www.researchgate.net/profile/Peter-Davis-4/publication/311928191_Regression-Style_Models_for_Parameter_Estimation_in_Dynamic_Microsimulation_An_Empirical_Performance_Assessment/links/5f2e7677a6fdcccc43b32661/Regression-Style-Models-for-Parameter-Estimation-in-Dynamic-Microsimulation-An-Empirical-Performance-Assessment.pdf"
title: "McLay 2015 - Regression - Style Models for Parameter ..."
type: "literature"
status: "in-progress"
year: "2021-11-02"
---

# Key Points

> What are they key takeaways from this literature
- Compare 6 types of regressoin models, their assumptions, and perform empirical assessment. OLS, random effects, fixed effects, mixed effects, dynamic panel model (GEE?). 
- Assess by proximity of fit between observed and simulated data. Found all models violated their assumptions but usually were a reasonable approximation.  
- OLS simple but effective. Fixed effects hard to apply due to lack of time variant variables. Random effects is good but lacks ability to respond to new information. System GMM is complex and works poorly but may be improved. Hybrid model ranked low despite performing good overall prediction. AR(1) model was bad due to it being misspecified. 

# Motivation

> Why was this literature written what problem is it addressing?
- DSSM dynamic microsimulation. looking at discrete time rather than continuous. Discrete variables are usually easy to model using transition tables calculated ia logistic regression. Continuous variables are more difficult. also use regressions as well as other optimisation algorithms. 
- The choice of model to use is not simple but is rarely discussed. Models should meet their assumptions but are rarely checked.
- If model is a poor approximation can greatly inflate errors.
- A model should be tailored to the needs of the microsim. Do simulated data reflect reality? Can also possible scenrios be performed? Cant discern much otherwise.
- Comparison of models in literature is rare. Develop microsim to assess the performance of 6 candidates. Although analysis is bespoke to the dataset can be somewhat generalised.


# Background

> What previous work has been done towards this problem?
- Most Msim transitions are designed to produce consistent individual trajectories over time. 
- This work focuses on regressions commonly used elsewhere. Looks at lagged OLS (OLS-LDV), random effects, fixed effects. Also using AR(1) model, combining fixed and random effects, a dynamic panel general method of moments (GMM). 

# Methods

> What methods were used? How do they address any issues?
## Regression types
- OLS-LDV is a standard regression with lagged covariates.  Assumes there are no individual (random) effects. Everyone has the same intercept. In longitudinal data this is unrealistic. there will be individual effects. this does not hold with lag variables included. OLS model is dynamic such that it can quickly react to changes in predcitor values.

- Random effect models assumes  there are individual effects. There are individual level effects. Each individual is assigned an effect adjusting their behaviour. These effects usually satisfy a normal distribution. This model assumes individual level effects are not correlated with predictors. They will oscillate randomly about their effect overtime ignoring any variable changes. These data are coherent but slow to change. Assumes individual level effects are not correlated with other predictors. Hausmann test can check this. Also assume observations are independent from each other. Again unlikely given longitudinal data.
- To resolve this employ an AR(1) correlation structure in another model. Will relax independence assumption. 
- Another major decision is how to assign individual effects (what groupings). Richiardi papers discuss this (1).

- Fixed effects model tries to resolve correlation between individual effects and predictors. Looks at within person variance and fits a  model for change on particular predictor. Each individual gets their own regression. (Isnt this a random slopes model and not a fixed effect model?). Drawback is cannot predict mean fixed effect of a time invariant predictors (e.g. gender). 

- hybrid model is a mixed effects model. honestly this paper seems to be overcomplicating this. Model both fixed and random effects simultaneously. Mean and distribution of a predictor. 

- as lagged variables are endogenous can use instrumental variable analysis as well. Simplest way is 2 stage least squares (2sls) but assumes homoscedasticity. General method of moments (GMM) can be used instead. Difference GMM transforms predictors by differencing and uses lags of predictors as instruments. Does not estimate for time invariant variables. System GMM does allow for time-invariant variables by further stratifying instruments by desired levels. Assumes that differences of instruments do not correlate with individual effects (stationarity). Test using Difference in Sargan test (3). 

- to summarise. OLS-LDV is a regression with lag variables. doesnt satisfy IID accumption. Random effects model gives everyone a unique constant probability of transition. Assumes observations independent and no correlation with predictors (unlikely). Fixed effects model gives each individual a linear slope over time. Cannot estimate effects of time invariant predictors. AR(1) model adds correlation structure to relax independence assumption for random effects. Hybrid model combines fixed and random effects and is the best option if hard to fit. System GMM allows for estimation of endogenous variable effects by using instrument variables. 

## Assessment methods. 
- Uses Modelling the Early Life Course (MELC) microsim dataset for nutrition in NZ (see figure). Test models using 2-fold cross validation.　Training data is used to calibrate model coefficients. Test data are used in microsim with calibrated coeffients over 1000 repetitions. 
- Compare observed and simulated microsim data using mean absolute difference (MAD), prediction sum of squares (PRESS), and cdf/qq-plots on the 1000 simulations. Repeat the whole cross validation process 30 times to get a distribution of overall performance. Can take a further grand mean of these 30 CVs for example.
- Significance tests used to test for differences in observed vs predicted means done using two-tail paired t-tests over cross validation sample of 30 MAD scores. For df=29 2.46 is the 99% critical value. 

![[Screenshot 2021-11-02 at 16.58.28.png]]
- 

# Results

> What was the outcome of the research? Was it successful?
## Assumption testing. 
- Several assumptions were tested for each regression. The required assumptions and their test scores are given. Most assumptions are violated if p<0.05.
	- No individual effects. Likelihood ratio test. Required by OLS model but violated (p<0.0001).
	- Individual effects independent of within child errors. Perasons correlation test. Required by random and mixed effects models. violated for both (p<.0001)
	- Individual effects IID. Assumption of randomly drawn individuals satisfies this. No spillover/hierarchies etc. Required by RE, AR1, and mixed effects models.
	-  Individual effects homoscedastic normal distributed. Shapiro-Wilk test on predictors of individual efects. Required by RE, AR(1), ME models. Violated (p<.0001) but look normal. 
	-  Exogenous time invariant predictors. Use Hausman test. Required by OLS, RE,AR1 models. satisfied in all cases (p>0.05).
	-  Exogenous time invariant predictors. C statistic from endogtest in stata. Required by OLS, RE, AR1, FE, ME. Violated by all methods/not available.
	-  Exogenous time variant predictors. C statistic from endogtest in stata ivreg2 or xtivreg2. Required in all but system gmm. Accepted for most predictors or unable to test. 
	-  within child errors uncorrelated. Arellano-Bond test. required by all but AR(1). rejected (p<0.0001) in all cases.
	-  no independence between within child errors. Pearson test used. required for all but OLS test. All rejected (p<.0001) or no convenient test
	-  Validity of moment condition for difference GMM. Hansen test. (p>0.05).
	-  Validity of moment condition for system GMM. difference in Hansen test. (p=.003)
	-  Stationarity of within child errors. Hadri and Larsson test. (p<0.05) in all cases.

- Ranking overall performance OLS>FE>RE>system GMM>AR(1)

# Glossary
Any new words should be defined here or reference from the main glossary in /Utility/glossary.  If there isnt a file in the main glossary you can still tag it here and create it later.
1. 

# References
1. Imputing individual effects in dynamic microsimulation models.  
	An application to household formation and labour market participation in Italy, International  
	Journal of Microsimulation,
2. 'Formulation and estimation of dynamic models using panel data',  Journal of Econometrics, 18, 47–82.
3.  'How to do xtabond2: an introduction to difference and system GMM in Stata', The Stata Journal, 9(1), 86–136.
4.   'Another look at the instrumental variable estimation of error- components models', Arellano