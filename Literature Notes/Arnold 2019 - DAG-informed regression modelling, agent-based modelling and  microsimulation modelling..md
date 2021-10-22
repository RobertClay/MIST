---
aliases: []
tags: [Microsimulation, ABM, CausalInference, Epidemiology, Counterfactuals]
author: "Arnold K"
url: "https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6380300/pdf/dyy260.pdf"
title: "Arnold - DAG-informed regression modelling, agent-based modelling and  microsimulation modelling. A critical comparison of methods for causal  inference"
type: "literature"
status: "in-progress"
year: "2021-10-22"
---

# Key Points

- Microsimulation models (MSM) and Agent Based Models (ABMs) are methologically similar. ABMs rely on individual agency and interactions to model emergent phenomena. Microsimuation focuses on independent movement of individuals under forced policy change.
- Directed Acylic Graph (DAG) based regression modelling is used in causal inference to model fixed causal effects where as microsimulation focuses more on random structures.
- DAGs may supplement ABMs to deal with greater complexity scenarios where things such as interactions and spillover effects are unavoidable.
- DAGs and ABMs sit on a spectrum weighting the importance of data vs theory. DAGs rely purely on data whereas ABMs rely heavily on theory. MSM sits somewhere in between and may be able to bridge the gap between them.


# Motivation

- While DAGs are useful in estimating the causal effect of an exposure on an outcome they are limited in the modelling of complex systems include interactions, longitudinal effects, and so on. In fact there are scenarios in which DAGs cannot suitably represent
-  Micromodelling systems such as ABMs are proposed as a potential alternative for investigation of coutnerfactuals. However they are mostly confined to other research areas such as social sciences.
-   This paper defines the differences between ABMs, microsimulation, and DAG regression modelling. 

# Methods

There is no specific method used here. This is a review of three fields:
- Agent Based Models
- Microsimulation 
- DAG modelling

# Results

- While methodologically similar these three techniques vary in their application. 
- DAGs are framed in the traditional epidemiological sense of cause and effect. They are limited by available data to certain timescales (usually months or more) and contexts. They also model the fixed effect of an exposure and struggle to incorporate individual heterogeneiety.
- ABMs are particulalry useful in measuring interactions between individuals scaling up to larger scale aggregate pheomena. Unlike DAGs they typically have limited data input at the expense of validity. They typically operate on much higher granularity compared to DAGs. Research questions are typically posed in terms of hypothetical interventions. If a person lifestyle is changed then what is the result on an outcome. It is expensive to do this kind of prospective study with the observational data required for a DAG.
-  MSMs are similar to ABMs here. They also have high granularity and work in interventions. The key difference is that interaction focused ABMs are more suited to social phenomena. This modelling of non-linear complex behaviour however can struggle to produce long term detailed forecasts desired for policy making. This is where MSM shines.

# Glossary

Any new words should be defined here or reference from the main glossary in /Utility/glossary.
1. 

# References
1. "https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6380300/pdf/dyy260.pdf"
