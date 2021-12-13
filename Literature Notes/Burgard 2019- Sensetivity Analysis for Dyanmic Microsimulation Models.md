---
aliases: []
tags: [dynamic_microsimulation, sensitivity_analysis, germany, health, care]
author: "Burgard Jan Pablo"
URL: "https://www.econstor.eu/bitstream/10419/207047/1/1679107933.pdf"
title: "Burgard 2019- Sensetivity Analysis for Dyanmic Microsimulation Models"
type: "literature"
status: "nascent, in-progress, gardening"
year: "2021-12-10"
---

# Key Points

> What are they key takeaways from this literature
- Sensitivity analysis is the varying of each model input to see how much they influence an outcome.
- In microsimulation, this is done through variance based sensitivity analysis. The variance of an outcome is decomposed into variance due to each initial input. This allows for quantification of uncertainty and identification of potential problem modules.
- This paper measures the change in variance due to health care demand over different birth, marriage, and divorce rates. Also measures input due to monte carlo error and impact of using population weights or not. 
- Can see population weights dont contribute much to variance. Medium term divorces are most influential and long term births are most influential in terms of health care demand. Several interesting plots demonstrate this. 
- Need to be careful about interpretation of sensitivity. Can draw different conclusions under random sampling or different population weights. Need to consider both percentage and absolute variance due to an input in results. For example, importance of divorces in health care supply outcome changes with unweighted/weighted pops. 
- Can visualise these values in a number of ways including stacked histograms and chord diagrams to more clearly see relationships. Can struggle for high dimensional cases though. Better vis is needed..
# Motivation

> Why was this literature written what problem is it addressing?
- One major task of microsimulation assessment is quantification of uncertainty. Usually phrased in terms of confidence intervals and sample variance. Estimation of confidence explicit is impossible for DSIMS due to complexity. Monte Carlo sampling proposed instead.
- Sensitivity analysis for microsimulation is done by exploring reliability by varying inputs particularly in extreme cases. Also suggested to explore latent parameters to explore their plausability. Is there some omitted variable biasing transitions? However noone has currently provided a general strategy for analysis or visualisation of outcomes. Could sensetivity analysis be useful for debugging microsims to find problem components. Could it be used to emulate alternate policy.

# Background

> What previous work has been done towards this problem?

# Methods

> What methods were used? How do they address any issues?
- Some univariate outcome of a microsim $y$ can be written as a function of some $k$ inputs $$y = f(x_1,...,x_k)$$.
- Variance of $y$ can then be decomposed as influcence due to each of the $k$ inputs. This can be done at first order level to estimate main effects (first order sensitivity), second order to estimate interaction effects, and so on.. If $k$ is large this can be expensive. Instead the total effects for the $k$th variable may be used. This is the sum of main effects and interaction effects involving this variable. It gives a good measure of uncertainty due to it. These effects are usually defined as a percentage of the overall variance $var(y)$. Higher implies more uncertain.
- Microsim data uses synthetic population of germany from the 2011 census. Focuses on city of Trier with 100k inhabitants and 5k households. Closed population only with entry due to birth/death. 
- Transitions based on regressions and administrative data tables. 
- Has modules for fertility, mortality, household migration, partnerships, relationships, care, and eeducation. Aims to estimate univariate outcome for ratio of living alone in care. Household structure is a strong indicator of future needs and care expenditure. 
- Input factors vary state transition ratios for births, partnerships, and separations. Ratio of increased partnerships vs baseline for example reflected in transition probabilities. Overall there are 1080 possible combinations of inputs to test. 
- Due to Monte Carlo error many repeats of each scenario are run. Show graphs of change in outcome under each scenario using two envelopes for confidence bands and worst/best case scenario. Due to Monte Carlo the model seed is also considered an input along with interaction terms between other inputs. There are 31 components to the variance here.


# Results
![[Screenshot 2021-12-13 at 15.17.26.png]]
![[Screenshot 2021-12-13 at 15.20.46.png]]
![[Screenshot 2021-12-13 at 15.28.43.png]]
![[Screenshot 2021-12-13 at 15.47.04.png]]
![[Screenshot 2021-12-13 at 16.02.41.png]]
> What was the outcome of the research? Was it successful?
- See table above for sensitivites over time. Little error due to random seed implies stable microsim. Hard to visualisedirect comparisons over populations/horizons. Useful to do it in a stacked surface plot. (see figure). Can see change in importance over time. Also need absolute variance plots (figure 6) to show how much variance is being explained by individual factors.
- Initially population weights are the most influential followed by separations, and finally births. Although at start their is little variance so pop weights arent really that important. Long term births are so important due to knock on effects with lower workforce and overall care/partners supply. 
- Need to be cautious with interpretation however especially in compirsons over time. Weights arent that important as shown. Need to account for total and relative variance composition. 
- Next set of plots (figure 3) are for pairwise input variability. In first column weights are included as a factor. In second/third they are unweighted and weighted populations respectively. 
- It is interesting the interpretation of certain influences. in the first column holding births constant it initially seems partnerships are more important than separations if they are not dependent on the inclusion of survey weights. However in the second/third columns including weights leads to a much higher impact of partnership in the medium run than separations. Demonstrates the importance of population weights on results.   
- In terms of assessing second order interactions chord diagrams can be used to assess both second and third order influences. Similarly cannot infer much without total and percentage variance due to these terms. 

# Glossary
Any new words should be defined here or reference from the main glossary in /Utility/glossary.  If there isnt a file in the main glossary you can still tag it here and create it later.
1. 

# References
1.  http://www.microsimulation.org/IJM/V6_3/4_IJM_6_3_2013_goedeme.pdf Goedeme et Al. Testing the statistical Significance of Microsimulation Results.