---
aliases: []
tags: [transition, probabilities, p-values, significance]
author: "Wasserstein Ronald"
URL: "https://www.tandfonline.com/doi/pdf/10.1080/00031305.2019.1583913"
title: "Wasserstein - Moving to a world beyond 'p < 0.05'"
type: "literature"
status: "nascent, in-progress, gardening"
year: "2022-02-08"
---

# Key Points

> What are they key takeaways from this literature
- p-values are misused and need reevaluating.
- Dont say statistical significance or similar. It is meant as a tool to determine whether an association warrants further research. Move towards treating p-values as continuous and to aid the 'science of learning from data, and of measuring, controlling, and communicating uncertainty'. 
- Do adhere to ATOMIC principles
	-  Accept uncertainty. P-values are not a definitive answer. Real world data is always noisy. Accounting for uncertainty involves better statistics through designs, sensitivities and better measures to improve rigour. Many studies should be considered in meta analysis.
	- Thoughtfulness. Design studies that are well planned and documented. This prevents rigging results and improves reproducibility. Be considerate of prior evidence, meaningful effect sizes, multiple techniques and approaches, and communicate modestly the confidence of results. 
	- Openness. Be completely transparent during the whole study.  Consult experts to assure best practice and clear presentation of design for other studies.
	- Modesty. Not overselling a study in combination with the above tempers expectations and clearly defines the impacts of a study - good or bad.

# Motivation

> Why was this literature written what problem is it addressing?
- A lot of don'ts with p-values
	- Dont base conclusion solely on statistical significance (p<0.05 or not)
	- Dont believe an association exists purely due to significance
	- Dont believe an association doesnt exist purely due to insignificance.
	- Dont believe p-value give proabability that chance alone produced the observed association or the probability the test hypothesis is true.
	- Dont conclude anything of practical importantce purely on significance
- Theres increasing momentum behind scrapping p-values altogether. However they need replacing with something else or statistics is a bit pointless.  American Stats Association (ASA) held an entire conference on this and authors summarised ideas in this paper. 

# Background

> What previous work has been done towards this problem?
- Don't say Statistical significance. The dichotomisation of p-values is a major issue. It should only be used to determine if an association requires further scrutiny.  Significance is not actually significant which says it all.  P-values should be treated as continuous and declared without comment when explaining results. Statistics is the 'science of learning from data, and of measuring, controlling, and communicating uncertainty.''
- To replace p-values there is no universal answer. There are however solid principles to adhere to.
- Accept uncertainty - Real world data will always be noisy. It makes perfect reproduction impossible. Must treat results as being incomplete. Must support uncertainty in conclusions seeking ways to quantify, visualise and interpret potential for error. Also tempers expectations of readers. Easiest way to do this is with standard errors or interval estimates but have similar dichotomy problems. (either 0 is in the confidence interval or is not.). Suggested to think of confidence interval as compatability intervals which use p-values to "show the effect sizes that are most compatible with the data under the given model'.  Doing this requires seeking better measures, more sensetive designs and larger samples to increase rigour of research. It helkps modesty and meta analytical thinking. Seek out replications and integration of meta analysis. Generally improves quality of stats
- Be thoughtful - Being thoughtful is to begin above all else with clearly expressed objectives.
	-  Recognise exploratory and rigid studies. Often rigid studies become exploratory. More flexible but less validity that is ultimately sloppy and hard to reproduce. Need to plan asking what are the practical implications of the estimate? how precise is the estimate? is the model correctly specified? Which naturally lead to three more Are modelling assumptions understood? are these assumptions valid? do results hold up under other modelling choices? This all needs documenting to allow critique and replication.
	-  Results should 'consider the purpose of the inquiry and compare best practice' and not falisify a null hypothesis. Rather ask what is at stake and determine what change is humanly/scientifically meaningful in context. Approach from practical benefit rather than statistical significance. More useful for complex organisms (schools, countries) and for increasing likelihood that observed benefits will be replicated in research and clinical practice.  In essence reliance on small effect sizes can be as problematic as p-values.  This is built on good data production through careful planning and execution. 
	- Consider prior knowledge and context. Declaring significance is useless without context. Look ahead to prospective outcomes in the context of theory and previous research. What do we already know and how certain is it? What effects are practically important? Naturally leads to using a lit review of evidence to identify practically important findings. 
	- Consideration of meaningful effect size. Fo this beforehand. It prevents over interpretation and is essential
	- Consider prior evidence, mechanism plausibility, study design, data quality, real word costs and benefits, novelty, and other research doman dependent factors.. and then p-values
	- Use a toolbox of techniques, employ good judgement, and keep up with developments. 
	- Consider multiple approahces for solving problems. For p-values, null p-values should be supplemented with p-values from a test of pre-specified alternative (e.g. minimal important effect size). Transform p-values into s-values (shannon information -log_2(p)). Second generation p-values that take practical significane into account. Null hypothesis is a composite representing a predetermined range of values that would be inconsequential. Value 1 suggests data support null hypothesis and 0  that data are incompatible with any null hypothesis. Anything else is inconclusive especially at 0.5.  Analysis of credibility (ancred) is an augmented confidence interval assessing its width and location of its bounds. Continuous p-values with false positive risk (FPR) answers is you observe a "significant' p-value what is the chance it is a false positive.  Goes on an on. Bayes factor bound. two stage p-values,  bayesian tools to provide a custom significance level. statistical decision theory. prediction of future observables. 
	-  Communication of confidence.  Dont be overconfident with confident intervals but treat them as compatability intervals (Greenland). "any researcher making a claim also gives their estimate of the chance it is true" is known as the confidence index. E.g. RR=2.4, p=0.03 says there is an 80% chance the drug raises the risk and 60% chance the risk is at least doubled.  Simple on paper but very controversial.  
- Be open 
	- Be open to 'open science' practicing public pre-registration of methods, transparency and completeness, shared data and code, and even pre-registered ('results blind') review. Completeness in describing all analyses and presenting all findings. Also includes understanding the role of expert judgement. Judgement is subjective but should be made as objectively as possible.  Personal decision making in analysis is unavoidable and trying to be purely objective results in pretending. Subjetivity must be a part of the solution and so expert knowledge is required.  Best way to do this is using established protocols (O'Hagan). 
	- Openness in communicating. Report continuous p-values as descriptive statistics. No universal answer for interpretation but depends on above mentioned contexts and study design/data/ etc.  Presenting multiple p-values should be done for other hypothesised values of variables of interest. e.g. 0 and minimum important effect size. s-value again a helpful alternative. or just bin p-values altogether.  Failing to be open results in selection bias for good p-values. Openness is that one study is rarely enough. Modesty in language is a good thing. Being open also provides enough information for research to be producible. 
- Being modest - statistics is often confounded with reality. Statistics is merely a thought experiement on the predictive performance of models. They can never emulate the true complexities of human systems. Being modest recognises there is no true model and as many should be thoughtfully considered as possible. For every experiment design there may be a better one. P-values, intervals etc. are all uncertain and should be stated as such. Statistical tools have their limitations. Statistical inferences modestly plays a minor role vs scientific inferences. Combined with openness report everything but do not over confidently interpret. Be modest in asking for others to reproduce work. Be modest in expectations. Be modest in different readers having different stakes in results and to be a neutral judge for every hypothesis.


# Glossary
Any new words should be defined here or reference from the main glossary in /Utility/glossary.  If there isnt a file in the main glossary you can still tag it here and create it later.
1. 

# References
1. Any useful references go here. If this reference has a note already link. If you'd like to add a note link it. Or just cite it normally.