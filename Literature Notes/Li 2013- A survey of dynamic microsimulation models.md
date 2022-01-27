---
aliases: []
tags: [review, dynamic_microsimulation]
author: "Jinjing Li"
URL: "https://www.microsimulation.pub/articles/00082"
title: "Li 2013- A survey of dynamic microsimulation models"
type: "literature"
status: "nascent, in-progress, gardening"
year: "2022-01-25"
---

# Key Points

> What are they key takeaways from this literature
- Authors review state of microsim assessing models developed and the methodological challenges they face. Ends with suggestionsnfor future direction of microsimulation. 
-  Paper has discuss some of microsimulations main issues. General issues such as base datasets, cohort or population, programming, and validation. Paper has discussed technical choices such as open or closed, alignment, behavioural response  to policy change, and links to ABMs.
- Many technical challenges to meet more complex and accurate policy analysis demands. CGE into microsims is one example. Behavioual responses and life cycle models for inter temporal choices. Networks of dependent indiviudals as in ABMs. Different units of analysis, resource constraints, and general parameterisation of policy need studying. 
- General field issues. Lack of documentation. High expectations can be allieved by transparency on implementation. New open source platforms are more open.

# Background

> What previous work has been done towards this problem?
- Most microsims developed using individual person data as thats what is available. some use business. 
- Dynamic microsimulation mostly used for projection of socio-econmic demogrpahics under current policy constraints.
-  More specifically for analysis of future cross-sectional data. Can also be used to assess individual longitudinal behaviour e.g.  pension contribution.
- Can also see spatial microsim
- Often used in tandem with macro models. micro can use macro for alignment. macro can use micro as initial conditions. 

There are a number of methological/structure choices that categorise dynamic msims outlined here
	-  base data type - Data quality is important but rarely does one dataset contain all desired variables. Often a combination of panel survey and administrative data are used. Admin data can be censored but have high sample sizes and few variables. Panel data is usually the opposite. Synthetic data can be generated to get the best of both worlds. General issues with datasets are highly contextual. Quality of imputation depends on many things [[Sterne 2009 - Multiple Imputation]] but produces square datasets useful in microsimulation. Synthetic populations are flexible wrt variables but require strong assumptions that make the untrustworthy. Often transitions are sourced from other datasets leading to transferability issues.
	-  Cohort vs population dataset- Is the whole populaton modelled or some specific sub cohort over a much longer time frame (e.g. all 51 year olds). Not really that important but adjusts model objectives.
	- Ageing methods - Defined as projecting a database forwards in time. Two types of ageing are static and dynamic ageing. Static ageing does not actually age individuals. They are seen as demographic blocks with some weight corresponding to the proportion of the real population they represent. Either the weighting or the block can be aged. Usually the weighting.  Dynamic does age individuals  either ageing the whole population one time step or each individual for their entire lives one at a time. Static ageing can estimate cross sectional distributions very well but does not account for individual behaviours. Only used in short <5 year forecasts. Dynamic ageing has no such problems but is difficult to implement and correctly calibrate. A lot of assumptions are required in practice that can bias outcomes. Misspecification errors are more common and dynamic msims require alignment in order to match aggregates. 
	- Discrete vs continuous - Two further types of ageing. Discrete ageing only occurs on discrete time steps. It is not actual ageing but rather a predicted snapshot of where an individual will be at a certain time. Usually represented as a number of transition matrices. Predictably the ordering of transitions is important here. Actually individual life paths aren't generated which is problematic for ordering of transitions. Cant die and then get married. Also discrete periods can be too large to sufficiently capture life processes. A yearly cycle cannot capture monthly events. Unemployment may be seasonal and certain diseases can have very rapid onset. Continuous models use survival times to model specifically when next event occurs. Have fewer ordering issues due to specific life trajectory mechanisms being well specified. Very hard to calibrate in practice due to lack of data that can capture limited complexity with respect to interactions between individuals and endogeneity. Harder to align too. 
	- Open vs closed - Can individuals leave/join the population or not. Open models are generally preferable as individuals can generate new spouses for example as desired and hence aged independently from each other. Interaction models are simpler. 
	- Macro-micro models - Microsims often interact with macro-economy via alignment computational general equiillibrium (CGE) methods (see “Iterated Top-Down Bottom-Up”).  Generally broader country state influences individual behaviour and vice-versa.
	- ABM hybrids - interaction between individuals rarely used in microsim and reserved for ABMs. Integration is coming but is expensive.

Review then goes into different methological practices used in certain areas of estimation and validation.
- Modelling transitions/behaviours - Structural models produced from statisical models or transition matrices. Behavioural models react to changes in market characteristics in order to  change behaviour of individuals. Structural models don't factor this in markets and are statuc with respect to policy. These models predict status-quo only.  Structural behaviour models are a mix of the two such that both individual and market variables effect next state. Labour market simulations are a good example here and repeatedly implemented in microsimualtion. 
- Alignment - Microsims drift due to misspecification errors in ageing processes. Alignment readjusts populations to match aggregates. Scott (2001) defines alignment as "a process of constraining model output to conform more  
   closely to externally derived macro-data ('targets')''.  Alignment is widely panned statistically but pragmatically necessary. Raises issues with consistency of estimates, level at which disaggregation should occur, and can bias model coefficients. Forces individuals to obey overall distributions which may no longer be true. It has been suggested (Klevmarken 2002) to  instead reformulate equations rather than constrain ex post (not sure what this means). Despite this alignment is common practice in microsim. Continuous variables are aligned in order to meet project averages or distributions. Binary variables are aligned with various methods e.g. multiplicative scaling, sideawlk, sorting algorithms etc. Microsims using historical datasets will align outputs with real data to create more credible profiles.
- Model complexity - More complex microsims require more variables to be included and more modelling. Can answer more questions over longer forecasts but harder to implement. Complexity can be a problem under alternate scenarios where model structure may not hold. Known as Lucas' Critique. Structural models can be more preferable here as they are more robust. Overfitting is another issue with more complex models. Too many variables can increase chance of multicolinearity or just include unnecessary variables. 
- Model validation - Validation is similar to estimation and testing but not very formalised. Should involve identifying sources of errors and thieir properties. (bootstrapping/Senseitivity analysis). Recommended areas to cover in validation (Morrison 2008 DYNACAN) in terms of context of validation, data validation/coefficient/parameter validation, code validation, module specific/multi-module specific and policy impact validation (micro-meso-maco level validation). Nowcasting is another popular method of validation due to use of real data. Most microsims are built on historic datasets as a result that are regularly updated. (See Understanding Society.). Another form of validation is using simplified models. If no future data is available to validate then compare to trustworthy simpler models (macromodels/ basic microsims that are reliable). It is however difficult to define what trustworthy is and this is ultimately inconclusive evidence.

 Programming of microsimulations is done with a number of languages:
 - General language (c/python etc.)
 - General stats package (stata/R)
 - Simulation modelling frameworks
	 - Modgen, developed by Statistics Canada (Wolfson and Rowe, 1998)  
	 -  LIAM2, developed by the Belgium Federal Planning Bureau (Bryon et al, 2011)
	 - UMDBS, developed by Sauerbier (2002)  
	 - GENESIS, developed by UK Department for Work and Pensions (Edwards, 2004)  
	 - JAMSIM, developed by Centre of Methods and Policy Application in the Social  
	 - Science (COMPASS), University of Auckland (Mannion et al., 2012)  
	 -  LIAM, developed by O’Donoghue et al. (2009))

Obviously using general languages is ideal. C++ is a favourite due to speed but is a lower level language and slower to implement. Using statistical/msim specific frameworks can remove a lot of the lower level programming and speed things up. However, hard to make generalised framework for all msims as they're highly bespoke.  

Progress overall of microsimulation is reviewed here too. An old msim DYNASIM from orcutt is used for comparison. It contained demographic, labour, tax,marriage, and a macroeconomic model for alignment. This model encapsulates what most modern msims use as well. There are a number of challenges described in implementing this model. These challenges can be broadly categorised into five different areas: behaviour response  
modelling (a-c), microdata quality (d), development cost (e), limited computation capacity (f) and model validation (g-h). Most of these issues are still highly relevant today ((Harding, 2007b)).  
- Many of the behavioural hypotheses in micro-simulation models are of insufficient theoretical and/or empirical basis  .
- Dynamic changes in the behaviour of the population are mostly not regarded by micro modellers  .
- The problems of including more than the primary effects of a policy programme is still unresolved  .
-  Quality and accessibility of the data required by micro models often are restricted severely.  
-  The development of micro-models frequently needs too much time and its costs are  accordingly high.
-  Running micro models usually requires a lot of computer time  
- The prediction quality of micro-models has not yet been systematically evaluated and validated  .
-  Large microsimulation models are so complex that they are difficult to comprehend and control.
Higher computing power, better datasets, and general frameworks address some of these issues. 

There are a number of obstacles in the advancement of microsimualtion due to 
- knowledge transfer- Most documentation is designed for use within teams and isnt general purpose. Knowledge is tacit and in unwritten rules lowering accessibility. Documentation is also poorly presented accross books and conferences. 
- model ownership - Many models are proprietary which also leads to lack of knowledge transfer. transparency is key.
- unrealistic expectations - Earlier models overestimated their ability. Microsims are then generally untrusted failures. Can only be used as general projections and cannot fully incorporate the human condition. 'All models are wrong, some are useful' in terms of planning and assessment of the worst case scenario. 
- funding - We all need more money. Microsims take a long time to develop beyond the usual 1-3 year postgrad contract. Leads to a lot of deprecation. 

Finally this paper suggests potential future directions. 
-  Model uses - Microsims are already widespread in their use. More fields will engage in msim too. Disease spread/financial planning are but two. Depends on data and methodology available. Mixture of simple and complex msims is needed. Focus on counterfactuals rather than accurate prediction of the future. As with ABMs the point is what ifs and worst case scenarios rather than accurate forecasting. Finally microsims can be used to better understand modelling of longitudinal behaviours. Lifespans of individuals not previously available can allow for better understanding of life decisions (e.g. fertility)
- Model assumptions - Most models are on one layer of individuals (people). Effort for socio-economics particularly to include houses, businesses as well. Relaxing the assumption of independent individuals is interesting as well. Seeing populations are networks usually reserved for ABMs due to computing power. Many microsims ignore realistic constraints such as budget and political capital. In reality there is not unlimited money for new policies and need for optimal practice. 
-  Methologies - 
	- A lot of methodologies used in microsimulation are annoyingly unwritten. Need formal documentation.  ". As noted above, this can impede the  
	progress of the field. Formally documenting the methods used and publishing in a peer-reviewed journal could improve the knowledge diffusion and increase the public good returns by academics, providing incentive to innovate." to do this and potentially reserve knowledge lost at end of funding.
	- Alignment is the most egregious example for lack of documentation. Error, manipulation, complex reweighting, random numbers etc. 
	- Models are generally estimated as modules and ignore any potential endogenous effects that may occur.
	- Lack of formal  docs for validation makes microsims hard to trust.
	- Many microsims only have one model run. Need an ensemble to build confidence intervals. 
	-  While DYNASIM documented many issues involved in the model  
	validation, there are still many areas that need to be explored, such as behaviour responses validation, longitudinal consistency validation, module interactions.



# Glossary
Any new words should be defined here or reference from the main glossary in /Utility/glossary.  If there isnt a file in the main glossary you can still tag it here and create it later. 
1. intertemporal choices - economics jargon for actions have consequences. Doing something now may change the decisions that can be made later. E.g. not eating now may make you hungry and eat more later.

# References
1. Any useful references go here. If this reference has a note already link. If you'd like to add a note link it. Or just cite it normally.