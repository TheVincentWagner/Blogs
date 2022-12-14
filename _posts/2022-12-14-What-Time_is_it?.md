---
title: "Blog post on: What time is it? Deep learning approaches for circadian rhythms."
date: 2022-11-12
---

### Disclaimer: 
All results presented herein are directly taken from the paper "What time is it? Deep learning approaches for circadian rhythms" by Agostinelli et al. published in Bioinformatics, 32, 2016.
	
## Motivation
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

## Data

There are unfortunately not enough real-world biochemical data sets that have been labeled as (a)periodic. The authors therefore supplement this real-world data sets with synthetic data sets, for which attributes like periodicity and potentially the period and amplidtude are known by construction. 
Synthetic data are specifically obtained using either Gaussian processes or algebraic formulas in combination with added noise.  
Together, all data sets make up BioCycle, a vast and comprehensive data base that is now only used but also curated by the authors. 

<img src="https://user-images.githubusercontent.com/59834752/207565278-f4744601-f887-4260-bbec-4be249ceadb9.jpg" alt="formula-based data" width="225"/> <img src="https://user-images.githubusercontent.com/59834752/207566453-037f5fea-915a-4605-99bf-437c27aa21f0.jpg" alt="Gaussian Process data" width="225"/> <img src="https://user-images.githubusercontent.com/59834752/207566609-a25962bf-37a8-439c-a8f5-98818b3e0462.jpg" alt="real-world data" width="225"/>
*Figure 1. Examples for each of the three subtypes of data.* Generally, periodic data are plotted in green, while aperiodic time series are depicted in ted. On the left, you see data originating from mathematic formulas. In the centre, sythetic data contructed by Gaussian Processes can be seen and on the right hand side, the real-world data sets are presented.

Here is the next paragraph.
