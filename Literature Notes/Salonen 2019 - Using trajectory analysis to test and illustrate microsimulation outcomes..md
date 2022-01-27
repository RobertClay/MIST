---
aliases: []
tags: []
author: "Janne Salonen"
URL: "https://microsimulation.pub/articles/00198"
title: "Salonen 2019 - Using trajectory analysis to test and illustrate microsimulation outcomes."
type: "literature"
status: "nascent, in-progress, gardening"
year: "2022-01-26"
---

# Key Points

> What are they key takeaways from this literature
- Propose a new way of visualising dynamic microsim data based on trajectory analysis. Assess group based trajectory analysis to identify unknown subgroups of a population.  
- Finite mixture modelling applied to longitudinal data can healp visualise life trajectories and classify individuals by mean behaviour. Useful tool in diagnostics of microsimulation validating against expected behaviour. 
- This paper applies trajectory analysis to the Finnish microsim of pensions ELSI to classify education, employment, and pension earnings states of discrete and continuous types. All three see clear classifications of behaviour indicative of socio-economic class.
- MIxture modelling is useful but constrained by computation time of EM algorithm and only useful for discrete ageing. It is a highly flexible tool handling many data types and widely implemented in software packages.
-  Future work could easily extend this analysis to stratification and better understanding of data generation within a population. 
# Motivation

> Why was this literature written what problem is it addressing?
- Dynamic msim results are often reported ex ante (based on forecasts) classification. It is hard to validate these projections without real data. There is a need for validation techniques. Validation is typically on cross sectional data looking at aggregate distributions of state rather than individual/group trajectories. 
-  Trajectory analysis offers advantages over this method. It can reveal latent patterns seen in longitudinal data. Can also distinguish variation between latent subgroups. 
# Background

> What previous work has been done towards this problem?

- Paper proposes two kinds of trajectory analysis. One stratifying over various labour state backgrounds looking for subgroups. Another looking to classify trajectory groups by some background factor (e.g. labour state) giving ex ante classifiers. 
- Population heterogeneity is desired in microsimualtions. Trajctory analysis can demonstrate this. Alows for analysis of any microsim outcome with interesting heterogeneity. Looks at a number of economic trajectories in the Finnish ELSI model. 
- Trajctory analysis is also well implemented in software packages. It can analyze many members of the exponential distribution family. IT is flexible enough to apply to both cross sectional and longitudinal data. It is however usually limited to cohort studies and discrete ageing. 
# Methods

> What methods were used? How do they address any issues?
- Trajectory analysis is the application of finite mixture modelling to longitudinal data. It is used for modelling unobserved heterogeneity of individuals longitudinally. A mixture is a weighted sum of (usually normal) probability distributions used to represented poly-modal distributions. 
- Two subtypes are growth mixture modelling and group based trajectory modelling. Both measure and explain differences accross individuals over time.  They differ in how they model heterogeneity. 
- Grow mixture models depict the average trend  of outcome and individual specific variation around the average trend with random effects.
- Aim of trajectory analysis is to identify groups of individuals each with the same unknown development profile. MSIM is then split into subpops with marginal probability distributions of outcome over some time periods. An individual will have some vector $y = (y_1, ..., y_T)$ of measurements over $T$ time points. The joint distribution of this trajectory is given as $f_i(y_i|X_i)$. If the individual could belong to any of $K$ subgroups then the density is a mixture of trajcetory weighted densities
	$$ f_i(y_i|X_i) = \Sigma_{k=1}^K \pi_kf_{ik}(y_i|X_i), \hspace{16pt} \Sigma_{k=1}^K\pi_k = 1, \hspace{16pt} \pi_k>0.$$
Where $f_{ik}(y_i, X_i)$ is the density of the trajectory given it belongs to the $k$th subgroup with weighting $\pi_k$. The choice of trajectory density here can vary based on data type. It is typically binomial/normal distributed for discrete/continous data. The weights and parameters of the associated densities (mean/variance for normal) need to be estimated using the Expectation Maximization algorithm . This is a two step algorithm numeric optimisation algorithm. E step finds expected log likelihood given current parameter estimates. M step calculates new parameter estimates given log likelihood. Goes back and forth until convergence. In this context the weights are being estimated. E step calculates the posterior density for subgroup membership (the weights). M step calculates MLE estimates for weights. The results is a vector of weights that classifies individuals into certain subgroups with the highest probability. 

How to define these groups is difficult. Often the number is varied choosing the set with the best information criterion. Bayesian Information Criterion used here (BIC) is used here. Can also use average posterior likelihood (<0.7 is a 'satisfactory' model).  Also common sense.

Missing data considered MCAR (what? strong assumption with no proof.) such that statistical packages can impute missing data.

# Results

> What was the outcome of the research? Was it successful?

Application to ELSI finnish microsim estimating groups in education and employment and pension. Chose k= 6, 5, 5 respectively. 

Can see clear groupings in employment state. One group clearly employed their entire lives until retirement. Partial employment groups are more nuanced and could occur for various reasons. Disability/ starting/ low education/deat for example. 

There is a clear misspecification error in results as earnings spike around age 65 for all groups. Lead to recalibration of ELSI earnings module due to people going back into work after drawing their pension which is rarer than estimated. 

Multinomial education state is also analysed. Seeing clear behaviour such that education attainment stagnates by 40. Different groups represent different level of educational attaiment. See high education individuals who mostly get masters degrees before 30. Likewise low education groups who rarely go beyond secondary education. 2% of pop are 'late bloomers' who get rapidly increase education state in mid 30s but could just be poor data. Could be classified further e.g. by socio-economic state.

Finally continuous pensions variable. Again seeing clear classification of groups. Classes who take disability pension early. Classes that lives a long time and see highest pension recieved. 



# Glossary
Any new words should be defined here or reference from the main glossary in /Utility/glossary.  If there isnt a file in the main glossary you can still tag it here and create it later.
1. 

# References
1. Any useful references go here. If this reference has a note already link. If you'd like to add a note link it. Or just cite it normally.