---
aliases: []
tags: [missing_data, multiple_imputation, hot_decking, imputation, edited_data]
author: "Andridge R."
URL: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3130338/pdf/nihms299474.pdf
title: "Andridge 2010 - Review of Hot Deck Imputation for Survey Non-response"
type: "literature"
status: "nascent, in-progress, gardening"
year: "2021-10-28"
---

# Key Points

- Hot decking handles missing data by replacing it with data from the nearest possible match. It imputes real (realistic) values, avoids strong parametric assumptions, can incorporate covariates, and provide good inferences for non-linear statistics when properly imputating uncertainty. It requires good donors unlikely in smaller sample sizes.
- Adjustment cell methods are simple but limit the auxilliary information and assocation that can be included. Alternate distance metrics can do much better. particularly predictive mean metric. 
- WHen choosing variables for donor pools they should be predictive of the imputed variable. Response propensity scores are useful for reducing bias only if it is associated with Y. Variable selection could determine this. 
- For multiple missing data, chioce of a single metric ignores associations. How to tradeoff between better prediction of individuals or associations requires further work (as of this paper?). They would yield consistent estimates if the model for variables being missing or propensity scores is incorrectly specified. See penalised splines of propensity for prediction.
- For 'swiss cheese' style randomly missing multiple data. Use of cyclic p hot decking again needs future work. 
- Obtaining valid inference from imputed populations is difficult. Using many imputed samples as in MI is advised to adjust for underestimated standard errors. 
- Hot decking is very useful for MCAR but needs more research into MAR and MNAR cases. 

# Motivation
- Missing data are a problem in large scale surveys.
- There is little consensus on best practices when applying hot-decking.
- This paper reviews different approaches including that of the US census providing potential areas for research.

# Background

> What previous work has been done towards this problem?
- a recipient will receive information from a donor using hot-decking. this recipient can either be randomly drawn from a pool or determinisitcally chosen (e.g. via nearest neighbour.)
- CPS invented hot-decking (1) using sequential adjustment cell method. NCES education agency also uses it. Most surveys use hot deck, cold deck, or bayesian imputation.
- Applied in medicine too but usually parametric hot-decking is preferrable.
- 
# Methods
## How are donors generated.
> What methods were used? How do they address any issues?
- All hot-deck methods draw a donor from a pool. There are many ways to do this
	- adjustment cell methods. individuals are binned into categories by demographic and a donor will receive from its own block. (CPS-ORG, Bollinger and Hirsch) does this. Starts with fine blocks and zooms out until a donor is found. Some branching algorithms can define blocks too (CHAID/CART). Can result in donors being overused so there are usually caps to the number of usages. Variables to categorise by are chosen depending on if they are associated with the missing variable or the indicator of a variable being missing (i.e. the propensity to respond) (see image below). high association with both is ideal for reduction in bias. Cells should be made that are homogenous with respect to both these variables.
	![[Screenshot 2021-10-29 at 10.27.59.png]]

	- instead of grouping by cells can group by a distance metric. indicator functions are similar to cells. things like maximum deviation or mahalanobis distance are used for continous variabes. regression is also a common choice. more complex metrics can combine continuous and discrete variables. If a regression with all categorical parameters is used it reduces to cell adjustment anyway. Regression is more useful as it chooses by influential variates where mahalanobis does not. Choosing a set of donors for a given metric is the next part. A cutoff is easiest. some group of k donors is drawn from. if k=1 its deterministic nearest neighbour canada's GEIS uses this. some models use all possible donors and inverse proportional weighting. incorporating propensity to respond is also useful propensity stratification will estimate probability of a response using a regression. Propensity scores can be used as a metric on its own or combined with the above usually regression. predictice mean metrics are prefereable though. 
	- Hot deck imputation is also used for editing contradictory complete data. Tradtionally this is a lot of if else statements and shuffling til they all pass. FH Algorithms have been developed since (2) that correct record with the smallest number of moves, abiding by constraints, and preserving distributions (GEIS again). Nearest neighbour is also used for editing imputation.
	- 
## Sampling Weights
- The weighted sequential hotdeck was developed because the unweighted version is biased if weights are related to the imputed variables. Often a donor would be used many times inflating variance. Sampling weights allow for all complete data to be a donor and limit repeated use. They are rarely used in practice though.

## Multivariate missing data.

- Often there is more than one missing value. There are many missing data patterns for this. Two pattern is similar to univariate case. All partial individuals are missing the same variables. Monotone is another common one where one missing variable implies a larger subset is missing. "Swiss cheese" style indicates random missingness.
- For two pattern case a common approach is many univariate single partition imputations. Donor pools can be tailored but associations between imputed variables are not preserved. The single partition deck can be used that uses a multivariate predcitve mean metric (regression). Does preserve assocaitions but not tailored. P-partition hot deck conditions imputation of a variable on all other complete and missing variables. This is a middle ground that preserves some association while being tailored. Depends on if metric for imputed variables can capture associations between imputed and conditioned variables. Single and p partittion can be combined but not implemented yet.
- Monotone patterns missing vectors are imputed instead. also uses single/p partition or a copmbination of the two for future work.
- More general missing patterns are difficult to preserves associations/conditions. Cyclic p-partition tries to do this similar to a Gibbs sampler. full information common donor hotdeck, neighbourhoods defined by predictive means, joint regressions, residual analysis are some further examples given in this paper.

# Variance estimation

- Hot deck imputed population are analyised as if no data was missing. These approachs ignore uncertainty. THere are three main approaches to valid variance estimates. Explicit variance formulae that incorporate nonresponse, resampling methods such as bootstrapping, multiple imputation with many imputed populations. 
- Explicit variance formula can be derived in simple cases. Older methods make strnog assumption (MCAR) with more recent approaches relaxed to MAR. They are usually some weighted function of regression coefficients or cell means/variances.
- For single imputation it is difficult to estimate variance without violation of model asumptions. Resampling is a popular alternative. Jackknifing removes estimates one a time to test for robustness. This underestimates variance and has adjustments to compensate. Alsorts of extensions to stratified multistage surveys and weighted hot decking. see also balanced half sample mehtod and random repeated replication. Some drawbacks though. Requires indication of which values were initially non-respondents which is rare. also cnanot estimate non-smooth statistics. needs boostrap instead. again underestimates variance without adjusment. This method only requires consistent estimator of response probability, which is more likely to be available.
- For multiple imputation combine an ensemble of imputaed populations together. Estimated mean and variance is simply a mean of means. However using the same donor pool for all imputed datasets underestimates variance. Adjustments such as Bayesian bootstrap, Approximate Bayesian bootstrap. IThis allows users to easily estimate variances besides totals and means. Does require 'proper' imputation though and can be hard to implement.

# Results

> What was the outcome of the research? Was it successful?

- Example looks at NHANES III on nutrition that has been used to compare imputation methods elsewhere (3,4). Selected 16739 individuals with 8 complete variables (age, gender, race, household size, blood pressure, health rating, and bmi.).
- A sample of 800 were drawn for a 5% missing fraction. Created a propensity model to induce missingness such that complete case inference would overestimate population average blood pressure. used a logit model based on age, being a woman and mexican. 
- adjustment cell hotdeck , predictive mean hot deck, propensity cell hot deck, and parametric regression imputation are all used. 
- Applied single and multiple imputation for all methods. For single inference (SI)hot deck methods used a naive estimato, an exact formula, and the jackknife to estimate variance. SI parametric method used naive and bootstrap estimators.
-  Multiple inference used improper MI with 5 data sets, and proper MI with 5 and 20 datasets. Used the MICR package for parametric imputation. Used RMSE error metric for each imputation
-  All methods performed well for bias except complete case under propensity model demonstrating large bias and underestimation. Propensity strata had higher bias than adjustment cell or predictive mean but not significantly.
-  Naive variance estimator underestimate variance by 81-90%. Improper MI also underestimated. All hot deck methods had lower variance in MI than SI. MI with K=20 was only marginally better than K=5. 
-  This study shows parametric methods do not offer much improvement over predictive mean. 

# Glossary
Any new words should be defined here or reference from the main glossary in /Utility/glossary.  If there isnt a file in the main glossary you can still tag it here and create it later.
1. 

# References
1. U.S. Bureau of the Census. UN/ECE Work Session of Statistical Data Editing. Madrid, Spain: 2003. A  
   comparison study of acs if-then-else, nim, discrete edit and imputation systems using acs data.
2. Fellegi IP, Holt D. A systematic approach to automatic edit and imputation. J Amer Statist Assoc.  
	1976; 71:17–35\
3. Ezzati-Rice TM, Khare M, Rubin DB, Little RJA, Schafer JL. A comparison of imputation techniques  
	in the third national health and nutrition examination survey. ASA Proc Section on Survey Res  
	Methods. 1993b:303–308.
4. Khare M, Little RJA, Rubin DB, Schafer JL. Multiple imputation of nhanes III. ASA Proc Section on  
	Survey Res Methods. 1993:297–302.
5. 