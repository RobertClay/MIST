---
aliases: []
tags: [microsimulation, dynamic, norway, pension]
author: ""
URL: ""
title: "Anreassen 2020 - The dynamic cross-sectionalmicrosimulation model MOSART"
type: "literature"
status: "nascent, in-progress, gardening"
year: "2022-02-03"
---

# Key Points

> What are they key takeaways from this literature

- Mosart is a Dynamic Microsimulation for education, labour supply and pensions that has seen frequent use in Norwegian policy analysis. 
- Straightfoward cross-sectional discrete time design estimating ageing using modules with theory/evidence based deterministic movement and conditional logistic regressions. Modules for demographic, education, retirement, labour, income, pension and fiscal variables.
- Model is highly modular and allows for easy swapping of different modules that may implement different policies. 
- Very useful for policy makers due to its flexibility. Many aspects of this model are the bare minimum and easily facilitate more elaborate prediction


# Motivation

> Why was this literature written what problem is it addressing?
- Stats Norway wanted an MSIM based on other projects in UK/US etc.
- Designed to facilitate government planning by maintaining detailed database and status-quo forecasting long into the future. That behaviour remains constant is an urealistic assumption. 
- Model is widely used in estimating demographic distributions for pension policy. This paper presents MOSART's structure and applications.
# Background

> What previous work has been done towards this problem?
- Dynamic MSIMS are either longitudinal or cross sectional. Longitudinal ages one individual at a time through the whole model run. Cross sectional ages the whole population one step at a time. Cross sectional ageing allows for interactions between individuals where networks are required (e.g. spatial microsimulation). 
-  Cross sectional ageing requires discrete time steps. A population is aged precisely one year for example. This allows for constraints to be used on each time unit. Populations can then be aligned to match external data such as demographic projections. Adjustment is done using logistic regression.
- Weakness in discrete ageing is that time steps can be too large. If an event takes place in <1 year it will be ignored. A cancer patient may abruptly die for no discernable reason. 
- Discrete time models require ageing of variables be done in a certain order. MOSART does this too with a series of modules (demographic, education, retirement, labour, income, pension, fiscal).
- MOSART uses stochastic simualtion. Does this using logistic random variables (logistic transitions).  These variables are constrained to match expected numbers of transitions per year. Also uses variance reduction techniques (common random numbers?). Helps reduce uncertainty due and increase statistical power of policy estimates.
- Modular system allows for easy swapping of pension systems. They have a few they use but is easily generalisable to many strategies. 

# Methods

> What methods were used? How do they address any issues?

- Written in C#. Uses 1Tb 64 core pc. A lot of work into memory usage and paralellesing operations. For example people with the same variables dont need their transition probs calculating twice. Theyre the same number. 
- MOSART uses Norwegian admin data from as early as the 1960s. Data is harmonised to include new variables and merge multiple readings per time step.  Also use preprocessing to make the  'initial population'. Missing data is imputed. Data is split into strata for quicker run times. Can also produce a fraction of the total population up to 0.01% for testing. 
- Births, deaths, migration are all easily aligned to match projections. They are a function of cohabition and marriage status. 
- Fertility is estimated on age, number of children, cohabitation and educational activity. 
- Mortality focuses on relationship between death and socioeconomic status. Based on death data for 2001-2010 using a logit model. Uses 
	- education, disability, family status and spatial county as factors 
	-  interaction terms with the above and age.
	- variables based on longevity of parents based on gender and age or death time.
	- alignment with external life expectancy. 
  Mortality is quite volatile and requires a lot of repetitions before a precise enough confidence interval. 
- Migration is by gender, age, current region, and region of origin. Immigration also depends on differences in unemployment rate, income per capita, number of previous migrants, and growth in population between three areas. Western europe/anglosphere, eastern europe, and the rest of the world.  Emmigration also depends on period of residence. They are used as exogenous inputs to the microsim (I.E. the number of migrants is decided year on year, the population is updated and then aged.). Generation is individual migrants is very difficult here particularly for education. Uses a number of surveys as sources. 
- Marriage is a series of transition dependent on gender and marital status. Complex interactions depending on any potential suitor. Usually of similar age. More complex lifestyle matching isnt included here. 
- Education is highly influential in this model. MOSART predicts 28 total states ranging from secondary up to PhD. Education is transition similarly to the Danish Dream model. Students can transition conditional on if they are already enrolled, dropped out, or will be going into education. Again uses logits based on individual histories and attributes. (series of logits seems wierd here. Its a multinomial state?). Migrant educations are partially missing but being improved. There is a general increasing in higher education attainment but that was not found here. May be issues between number of students and number of university places. Hard to separate the two without a population of universities too. 
- Retirement. Norwegian pensions must be drawn before they stop working. Some entanglement with labour modules as a result. There are several categories of retirement based on not retired, old age, disability and work assessment allowances (WAA). WAA is essentially a transitionary period before a disability pension. Disability pension varies depending on level of disability (50-100%). They form a 4 state markov chain. People usually move not retired-> old age. People who move to WAA usually become disabled and dont fully recover. Those in disability pension can move to old age pension.  Transition from not retired to old age is more stochastic depending on age, gender, disability states. Minimum age is 62. Usually by 67. 
- Labour supply predictably projects future jobs. Projecting labour supply is a concept based on the basic amount in the national insurance scheme (approx. 10100 euro  (1 BPU) as of 2019). Labour force participation is the probability of earning  >= 1 BPU in a given year. Predicted using a number of factors Age, gender, cohabitation, children, education, pensioner, stable career, length of time out of workforce. Long term histories hard to include for migrants. Stable career is a boolean depending on if a person has been in constant work since 23. It is a strong indicator of employment and disability. The participation rate is aligned to match externals. One policy example is shown here simulating higher participation rates and postponed retirement.  Both of which are significant. 
- Yearly income used to assess sustainability of pension systems.  Complete income trajectories can be used for a variety of outputs. . Income is adjusted yearly with trends removed. Log income is estimated using age, gender, cohabitation, children, education, seniority, stable career, pensioner, length of time unemployed. Data used for estimation is longitudinal and includes observation year. Two residuals in income estimation. One for permanent effect due to unobserved variables. Other is random white noise. (What? mixed effects model? How do you separate the two.). Permanent residuals depend on previous employment history. Unemployed people draw permanent residual from kde of other permanent residuals. Otherwise based on residuals from previous income. Currently very crude. Main challenge is heterogeneity and general oversmoothing of behaviour. Too much complexity going on.  Plan to estimate permanent residuel using AR-1 model instead. Clearer basis and based on cohort histories instead of combinations of cohort and yearly effects. Closer to Mincer equations  looking at income shocks. 
	- Pension expenditure is one of most detailed parts of MOSART. uses a number of labour participation and income rulse to calculate benefits for every individual. Creates distributional effects of  income and pension expenditure from different policies. Details are well explained in older papers (fredrikssen et al 2017.).  Very good estimates but struggles with special groups migrants, widows, disabled with large uncertainty in pension expenditure. 

# Results

- Some examples here of distributional differences in pension expenditure by 2050. Goes a bit off topic at this point. Lots of methology on how pensions models are built and how alternate policy changes results. 
	![[Screenshot 2022-02-03 at 15.13.28.png]]




> What was the outcome of the research? Was it successful?

# Glossary
Any new words should be defined here or reference from the main glossary in /Utility/glossary.  If there isnt a file in the main glossary you can still tag it here and create it later.
1. 

# References
1. Any useful references go here. If this reference has a note already link. If you'd like to add a note link it. Or just cite it normally.