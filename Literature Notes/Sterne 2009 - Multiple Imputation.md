---
aliases: []
tags: [missingness, multiple imputation, statistics]
author: Sterne JAC
URL: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2714692/
title: "Sterne 2009 - Multiple Imputation"
type: "literature"
status: "nascent, in-progress, gardening"
year: "2021-10-25"
---

# Key Points

> What are they key takeaways from this literature
- Multiple imputation is a technique for reducing bias due to missing data. This paper describes its pros, cons, and applcation to general medical journals.
- Multiple imputation will randomly assigned missing values to an ensemble of populations. Each population is fitted with a model and the overall effect analysed.
- While useful it suffers a number of pitfalls. Namely if data are incorrectly assumed missing at random, if variables are not Gaussian distributed or if any variable being imputed is conditional on the outcome.
- To prevent this guidelines are specified. The user should:
	- describe any missing data giving possible reasons in terms of other variables if possible
	- Clarify any differences between complete and imputed populations.
	- Describe the analysis done in great detail. If Multiple Imputation is used describe its assumptions (missing data MAR), parameters (number of imputations), software, variables imputed, and robustness under sensetivity analysis. 
- Very few papers as of 2009 follow these guidelines. Only 1/59.

# Motivation

> Why was this literature written what problem is it addressing?
- Most studies have missing data that undermine validity of results leading to bias in clinical research.
- Research usually simply ignores any entries with missing data. This excludes a portion of the original sample and can lead to bias.
- Risk of bias depends on why the data are missing. Missing data falls into three types:
	- MCAR missing completely at random. As the name suggests these missing values are truly random and do not depend on any individual attributes.
	- MAR missing at random. There is observed systematic missingness in the data. Perhaps someone with low cholesterol is unlikely to attend a follow-up appointment. 
	- MNAR missing not at random. There is unobserved systematic missingness. Perhaps cholesterol is unobserved and we have no idea why individuals go missing. It is impossible to distinguish between MAR and MNAR using observed data. You would need to know the missing values of x in order to determine why it is missing. For example, if x<1000 indicated low blood pressure/missingness how would you prove this if you didnt know what x was.

- MCAR does not induce bias. MAR does induce bias but can be corrected for using techniques such as multiple imputation. MNAR can be addressed using sensitivity analysis to understand the missing data mechanism (1). 

# Background

> What previous work has been done towards this problem?

- There are numerous ad-hoc approaches to dealing with missing data.
- Replacing missing value with imputed values such as means, using a missing category indicator, last value carried forward, or simply dropping the missing rows. None of these are valid in general and lead to bias.
- Single imputation deflates standard errors and fails to incorporate uncertainty. Sensitivity analysis that imputes a variety of single values can be more useful if intensive.
- Missing data in predictors unrelated to the outcome can be assessed using specialist methods but this is not required.
- Data that is MAR can be assessed using more powerful analyses.  Random effects models incorporate information on partially observed variables from intermediate time points (2, 3, 4) or bayesian methods (5). Other approaches include weighting analysis to allow for missing data (6), and MLE estimation (4).

# Methods

> What methods were used? How do they address any issues?
- Multiple imputation is a general approach similar to single imputation. It incporates uncertainty in missing data by using an ensemble of numerous plausible missing populations. 
- The first stage is to create multiple copies of the dataset with missing values imputed. They are sampled from some predictive distribution based on observed data in a bayesian fashion.
- The second stage uses statistical methods to fit a model of interest to the imputed datasets. An ensemble mean and variance can be calculated via Rubin's rules.

# Pitfalls
- This is not a universal technique. It requires modelling distributions for all missing variables which can introduce more uncertainty. more specialist techniques may be preferable.
- MI may also induce bias if not implemented properly. There are a number of reasons for this.
- Omitting outcome variable from imputation procedure. Predictors are generally conditoinal on the outcome. Someone who develops coronary heart disease will have higher systolic blood pressure on average. This needs to be accounted for rather than imputing purely randomly.
- Non normally distributed variables. If a variable is not normally distributed this will skew the population and induce bias. There are futher techniques for non-normal distribution.
- Requires MAR assumption. If predictor of missingness is in the dataset this method is useful. If the data is MNAR it is not. MI will underestimate mean predictors and may produce spurrious associations. It is sensible to include a wife range of variables when imputing.
- Data not missing at random. Data that are not MAR. MI will be biased in this case. It is impossible to determine how big any bias is. The analyist must detemine possible reasons for missing data and the likelihood of it being a concern.

# Results

> What was the outcome of the research? Was it successful?
- Reports of application in general medical literature are included.
- 59 papers from (New England Journal of Medicine, Lancet, BMJ, and JAMA) used 'multiple imputation' in the text of the article. 36 reported at least some information on missing data. Only 7 fully reported comparisons of distributions between individuals with and without missing data. 
- 22 papers reported imputation based datasets. Results of both imputed and complete cases were fully reported in only 7. Only 1 used sensitivity analysis. It was rarely possible to see the impact for including missing data.
- Variables used in imputation were rarely listed, and the plausibility of MAR was rarely assessed.

- Suggested guidelines are as follows:
	- Report the number of missing values for all variables of interest. Give reasons for missing values if possible and indicate how many individuals were excluded from missing data as a result. Describe reason for missingness in terms of other variables if possible. 
	- Clarify whether there are differences between indivudals with complete and incomplete data. E.g. by providing descriptive data for distributions of each.
	- Describe analysis used to account for missing data (MI) and any assumptions made (MAR)
For MI specifically:
	- Report the software used.
	- Report the number of imputations
	- What variables were used in the imputation.
	- Where possible provide results solely from complete cases and explain any differences.
	- Discuss whether variables included satisfy MAR assumption
	- Investigate robustness of inferences using sensetibity analysis from MNAR techniques ().

Attached is an example of use of MI in a chemotherapy study done mostly right.
![[Screenshot 2021-10-25 at 18.21.38.png]]

# Glossary
Any new words should be defined here or reference from the main glossary in /Utility/glossary.  If there isnt a file in the main glossary you can still tag it here and create it later.
1. 

# References
1. Resseguier N Sensitivity Analysis When Data Are Missing Not-at-random
2. Carpenter JR, Kenward MG. MAR methods for quantitative data. In: Missing data in randomised controlled trials— a practical guide. 
3. Goldstein H, Carpenter J, Kenward MG, Levin K. Multilevel models with multivariate mixed response types. Stat modelling (in press).
4. Schafer JL. Analysis of incomplete multivariate data. London: Chapman and Hall, 1997.
5. Scharfstein DO, Rotnitzky A, Robins JM. Adjusting for non-ignorable drop-out using semiparametric non-response models.
6. Carpenter JR, Kenward MG, Vansteelandt S. A comparison of multiple imputation and inverse probability weighting for analyses with missing data.
7. Demirtas H, Schafer JL. On the performance of random-coefficient pattern-mixture models for non-ignorable drop-out.
8. Carpenter JR, Kenward MG, White IR. Sensitivity analysis after multiple imputation under missing at random: a weighting approach

