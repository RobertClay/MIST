---
aliases: []
tags: [Microsimulation, Spatial, health, IPF, Simulated Annealing, bayesian, multi-level modelling, pattern orientated modelling]
author: Smith Diane
URL: https://www.mdpi.com/2571-8800/4/2/15
title: "Smith 20 Estimating Health Over Space and Time"
type: "literature"
status: "in-progress"
year: "2021-10-25"
---

# Key Points

> What are they key takeaways from this literature
- majority of health papers model non-communicable disease while communicable disease is more suited to ABMs.
- two general approaches to population synthesis similar to standard microsim treating areas as a demographic alongside age sex etc.
- Stochastic methods are becoming more prevalent due to ability to incorporate uncertainty.
- Next phase is to improve communication of what these models do to both other modellers and policy makers/the public. This is done through open source work and better visualisation.
- Not much said on spatial ageing in this paper.


# Motivation

> Why was this literature written what problem is it addressing?
- The review extends upon earlier reviews of spatial microsimulation as both a method and health application.
- health microsim used to better advise treatment policy that typically have some spatial component.
- In practice most datasets ignore spatial behaviour at the local level at which policy decision are made. Spatial msim simulates this.

# Methods

> What methods were used? How do they address any issues?

- literature search on pubmed and sciencedirect search engines. 
- Found a total of 21 relevant articles after removal of duplicates, irrelevant methodological articles, and other relevant papers outside the search were added.
- focus on a narrow range of issues. diet and smoking most prevalent. Gambling, mental health, alcohol, dental health, maternity, diabetes and mortality also included.
- These applications particulary focused on resource allocation and policy decision making.

- Several methods mentioned for how spatial microsim estimates small area effects.
- Bayesian techniques (3,4) and multi-level modelling (5,6) are most commonly used.
- For population synthesis Iterative proportional fitting and Simulated Annealing are the most commonly used. 
- IPF (10) assigns each member of a dataset a weight for their contribution to the total population in each area. For example a white 50 year old male may be assigned a weighting of 0.05 for Leeds. That is approximately 5% of the Leeds population is suitably represented by this individual. These weights are then adjusted until they match results from aggregate data such as a census.
- Simulated Annealing (11) assigns 'real' individuals to each spatial area. Usually a full population of synthetic individuals will be used. These individuals will be randomly moved between areas in order to optimise some goodness of fit measure. 


# Results

> What was the outcome of the research? Was it successful?
- No results its a review. 
- Conclude there are two main challenges with spatial msim.
-  Validation is difficult to do but multi-level regression coefficients as IPF inputs (2) and pattern orientated modelling (9) are potential solutions.
- Lack of interpretability of microsimulations to the public due to closed source code and poor visualisations. Doesnt say much on how this is being addressed.

# Glossary
Any new words should be defined here or reference from the main glossary in /Utility/glossary.  If there isnt a file in the main glossary you can still tag it here and create it later.
1. 

# References
1. https://www.mdpi.com/2571-8800/4/2/15
2. Whitworth A Estimating uncertainty in spatial microsimulation approaches to small area  
estimation: A new approach to solving an old problem
3. Congdon, P. Estimating diabetes prevalence by small area in England.
4. A spatial regression  
model for the disaggregation of areal unit based data to high-resolution grids with application to vaccination coverage mapping
5. Fat nation: Deciphering the distinctive geographies of obesity in  England.
6. Using geocoded survey data to improve the accuracy of multilevel small area synthetic estimates
7. Tanton, R. A Review of Spatial Microsimulation Methods.
8. Voas, D.; Williamson, P. An evaluation of the combinatorial optimisation approach to the creation of synthetic microdata.
9. Grimm Pattern-Oriented Modeling of Agent-Based Complex Systems:
10. Lovelace, R.; Dumont, M. Spatial Microsimulation with R
11. O’Donoghue, C.; Morrissey, K.; Lennon, J. Spatial Microsimulation Modelling: A Review of Applications and Methodo-logical Choices.