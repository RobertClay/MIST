---
aliases: []
tags: [uncertainty, reduction, common, random, numbers, CRN]
author: "Stout Natasha"
URL: "https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2761656/"
title: "Stout 2008 - Common Random Numbers for Disease Modelling"
type: "literature"
status: "nascent, in-progress, gardening"
year: "2022-02-07"
---

# Key Points

> What are they key takeaways from this literature
- Noise in microsimulations increases model repetitions and run time. Variance reduction techniques like common random numbers (CRN) can reduce variance and make microsimulations more efficient.
- CRN partially seeds individuals such that certain groups of events occur over repeat model runs. Partially seeded individuals are controlled to differ over the exposures of interest and reduce noise. CRN allows for more efficient model calibration but also direct comparison between repeats of an individual. A sample of one individual can be built up and compared.
- CRN is useful but need to be careful when hypothesis testing due to correlation between within individual measurements. Certain precautions such as specific correlation t-tests and Bonferroni correction are needed to ensure validity of results.  
# Motivation

> Why was this literature written what problem is it addressing?
- Disease simulations used to make decisions on treatment strategies. 
- As model complexity increases uncertainty grows. This noise can dominate sensetive differences in policy outcomes. Microsimulations (MSIMS) then have low statistical power and require a large computationally expensive sample size to provide sufficient evidence. 
- Variance reduction techniques are used to control uncertainty and reduce the sample of microsimulation repetitions needed. Common Random Numbers (CRN) is a popular approach for variance reduction disease modelling.  CRN also allows for direct counterfactual analyses at individual level in MSIMS.　Otherwise comparisons are done on approximate individuals or aggregates. 
-  This technique goes under the radar and this paper demontrates applications for benefits in analysis of breast cancer simulations. 

# Background

> What previous work has been done towards this problem?
- CRN dates back to the 1950s in engineering simulation. CRN is the coordinated or synchronised use of random numbers such that the same random numbers are 'common' to to the same stochastic events across all model runs. For example, a stochastic event may be the time of birth of a child to certain parents. Using the same random numbers fixes the birth to a specific time.  Life trajectories for this baby can then be more directly compared. 
- This yields model correlated in stochastic variation reducing overall variance in the distribution of model runs. It does not reduce variation within a single model run. For analysis at the individual level it reduces the number of model runs needed to produce stable estimates.
- To implement random number sequences are assigned to different stochastic events. For disease simulation the same sequences are used within individuals across model runs. This generates identical individuals while still generating unique individuals within a model. Individuals can produce a sample of themselves. 


# Methods

> What methods were used? How do they address any issues?
- Implementation of CRN is divided into design and designation phases. Events within an individual to be held common are identified and combined into gruops based on function. The second phase designates sequences of random numbers to each group. 
-  In this example women face breast cancer events including onset, progression, detection, treatment, and death. Events are classified into mutually exlcusive, independent groups based on their function in disease process, ordering, and conditionality of the event within an individuals lifetime. There groups are 
 woman and tumour level characteristics, symptom detection and determination of screening schedules and detection. Each group is assigned an independent sequence of random numbers. 
 - This allows women to have the same tumour progression repeatedly regardless of screening strategy. If detection occurs earlier then subsequent events in her life from different random number froups may be different. The random number for treatment effectivness in the first grouping may be different if the event occurs later in life. If desired, this random number can be synced such that treatment is the same dependent of age. Hence the tendency for a treatment to be ineffective in this simulated gruop is preserved. To implement this assign treatment effectiveness a separate grouping or reorder when random numbers are drawn. E.g. draw the random number of effectiveness at the start of a woman's life. 
 ![[Screenshot 2022-02-08 at 12.53.59.png]]
 - Designation phase then uses some random number generator (RNG) whose choice is considered here. Typically RNG produces a sample from a uniform distribution.  For CRN features are
	 -  length, Sequences need to avoid repeated patterns within a model run or individuals may not be independent from each other.
	 -  Reprocubility stems from having RNG with a seeded input. Unique seeds produce unique sequences. However this is hard to guarantee and often see similar sequences. again messes with independence. Seed values must be carefully chosen. 
 - Mersenne Twister and RngStream are two popular choices here. Very fast and have sufficient period length $(>2^{191})$ and widely implemented. RngStream slightly slower but better independence. 
 - To implement a stream is assigned to each group of events using the same initial seeds. Ensures commonality. Each individual then uses a subsequence of each stream for each group of events. Independent aperiodic streams should ensure independence. Alternatively each individual may have a seed which it inputs into an RNG generator to get a sequence. This sequence is divided for each individuals groups of events. Again a lot of seeds can induce dependence. There are many approaches dependending on how many streams to create and how to cut them. One approach uses just one stream and divides it by individual and group. 
	  
# Results

> What was the outcome of the research? Was it successful?
- Application is made in two cases for microsimulations of breast cancer. 
- Comparison at the population level (calibration) - Calibrating models requires estimating the distribution of unknown parameters through repeated model runs. Hampered by excess noise increasing number of repetitions. Compared model over varying repetitions with and without CRN. Can see reduction in number of reps needed for desired results. 
![[Screenshot 2022-02-08 at 12.59.35.png]]
- Second application is on individual level analysis. A simulated individual can be compared with themself. Provides a distribution in the difference between policy strategies.  Experiment compares woman diagnoesd with breast cancer with herself under infrequent/frequent approaches. Individuals were same up until first mammogram (missed or not) and then differences in life expectancies calculated. 92% of women dont benefit from frequent tests. 8% gain increased life up to 40 years. Some even lost life implying infrequent testing was beneficial (less stress?). Proves useful in individual level decision making. Most women dont see a change in life length indicating the value of a single mammogram. 
![[Screenshot 2022-02-08 at 13.07.40.png]]
- To understand variation from stochastic events need multiple repetitions over different random number sequences. CRN requires fixed sequences for commonality. These streams repeated use will produce correlated variability in differences in output over repeated model runs. Hypothesis testing needs to be done carefully. T-tests that account for correlation should be used rather than the standard tests that assume independence. 
- With or without CRN bonferroni adjustment for comparison amoung model runs can be done. Adjusts level of statistical significance to account for spurrious correlation. Leads to more conservative estimates in difference in model outputs due to correlation. 

# Glossary
Any new words should be defined here or reference from the main glossary in /Utility/glossary.  If there isnt a file in the main glossary you can still tag it here and create it later.
1. 

# References
1. Any useful references go here. If this reference has a note already link. If you'd like to add a note link it. Or just cite it normally.