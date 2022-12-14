---
title: "Blog post on: What time is it? Deep learning approaches for circadian rhythms."
date: 2022-11-12
---

### Disclaimer: 
All results presented herein are directly taken from the paper "What time is it? Deep learning approaches for circadian rhythms" by Agostinelli et al. published in Bioinformatics, 32, 2016.
	
## Motivation:
Circadian rhythms (CRs) play a crucial role in our everyday life - literally! The word circadian is directly derived from "approximately daily" and CRs therefore are a class of biochemical oscillaors with a period of approximately 24 hours. CRs can be found in animals, plants and funghi, all three kingdoms of life on earth.
Fundamentally, CRs (and many other periodic changes) are encoded by oscillating concentrations of specific molecular species like for example proteins. 
Fortunately, modern measurement technologies are capable of extractring ever more detailed data from biochemical systems, thereby reveiling rhytmic behaviour andother complex patterns. 
Still, measurements are expensive and therefore not taken at arbitrarily many time points and /or with arbitrarily many repititions. 
In addition, inherent noise corrupts the information content of produced data sets. 
While these are not all challenges, they are often sufficient to prevent the finding of reliable conlusions. 

As one nevertheless wants to leverage the data as well as possible, the paper aims to answer to relevant research questions:

* Is a biochemical species of interest periodically osciallting?
* Can we extrapolate periodic behaviour reliably from single time point measurements or scarse data in general?

The paper produced evidence, that both questions can adequately be answered using deep learning techniques, or to be more precise, Deep Neural Networks (DNNs).

