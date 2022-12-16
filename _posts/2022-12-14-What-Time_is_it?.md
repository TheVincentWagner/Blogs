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
* Can we estimate a measurement time point (and potentially future oscillating behaviour) reliably from single time point measurements or scarse data in general?

The paper produced evidence, that both questions can adequately be answered using deep learning techniques, or to be more precise, Deep Neural Networks (DNNs).

## Data

The data generally report or mimic transcriptome data. More specifically, the data reports which gene is read how often. This directly correlates with the production rate of the proteins encoded in some of the genes. It is worth noting that the number of genes under consideration is very large, potentially reaching 20 000 and beyond.
There are unfortunately not enough real-world trascriptome data sets that have been labeled as (a)periodic. The authors therefore supplement this real-world data sets with synthetic data sets, for which attributes like periodicity and potentially the period and amplidtude are known by construction. 
Synthetic data are specifically obtained using either Gaussian processes or algebraic formulas in combination with added noise.  
Together, all data sets make up BioCycle, a vast and comprehensive data base that is now only used but also curated by the authors. 

<img src="https://user-images.githubusercontent.com/59834752/207565278-f4744601-f887-4260-bbec-4be249ceadb9.jpg" alt="formula-based data" width="245"/><img src="https://user-images.githubusercontent.com/59834752/207566453-037f5fea-915a-4605-99bf-437c27aa21f0.jpg" alt="Gaussian Process data" width="245"/><img src="https://user-images.githubusercontent.com/59834752/207566609-a25962bf-37a8-439c-a8f5-98818b3e0462.jpg" alt="real-world data" width="245"/>
*Figure 1. Examples for each of the three subtypes of data.* Generally, periodic data are plotted in green, while aperiodic time series are depicted in red. In the left 4 columns, you see data originating from mathematic formulas. The central 4 columns depict sythetic data contructed by Gaussian Processes and the right 4 columns show real-world data sets.

BioCycle is the data set used to answer the first question. Similarly, BioClock is another data set created and curated to address the second one. BioClock also contains transcriptome information, but focusses on genes that are part of the core clock, the main time-tracking mechanism of most organisms. In contrast to approximately 20 000 gene expressions tracked in BioCycle, BioClock therefore only includes information for 16 genes.

## Methods

The authors evaluated the performance of several learning algorithms to tackle the two problems stated above. However, DNNs clearly won against all respective competitors. 
The resulting learning systems are named BIO_CYCLE and BIO_CLOCK which directly translates the data set names. 

<img src="https://user-images.githubusercontent.com/59834752/207595119-c95293ab-62b3-456d-b252-9d832f0da82b.jpg" alt="network architecture" width="480"/>

*Figure 2. Architecture of both learning systems presented in this work.*

We will first describe the learning system BIO_CYCLE that aims to solve the first research question. It uses gene information of one gene and several time points to output either a single logistic periodicity response or an estimation of the signal's period. The authors point out and describe, that and how a very similar DNN can also be used to estimate the phase, lag and amplidtude of a given signal.
The systems trains deep neural networks with 3 fully-connected hidden layers consisting of 100 nodes each. The training consisted of 50 000 iterations of momentum mini-batch gradient descent optimizations. The batch-size, or in other word, the number of considered data sets per iteration was set to 100. Furthermore, the learning rate of the network exponentially decayed wich a growing number of already performed training iterations. 

The system BIO_CLOCK, in contrast to BIO_CYCLE, is designed to answer research question 2. One big difference between the two systems is the choice of respective in- and output. BIO_CLOCK decomposes gene information of several genes at a single time point into the coupled sine and cosine of the oscillations phase angle.
The authors tried a variety of different network architectures ranging from 2 to 9 network layers with 100 to 600 nodes per layer. Again, an initial learning rate of 0.1 decays exponentially during the course of the training. Reliable results are obtained through the use of 5-fold cross validation over all BioClock data sets.

Is is worth mentioning that all used code is accessible for reuse and intended also for a purely biologically trained audience.

## Results
The DNNs trained in this work are compared to 4 existing methods (ARSER (ARS), Lomb-Scargle (LS), JTK_Cycle (JTK) and MetaCycle (MC)). 
We begin with results regarding research question 1: Is a chemical species oscillating or not?
As this question is a special case of binary classification, receiver operating characteristic (ROC) curves are a good measure for the quality of different solutions. 
In essence, ROC curves compare the true positive rate to the false positive rate. A completely random classifyer would therefore be equivlent to a straight diagonal line from (0,0) to (1,1). The better the classifier is, the more this curve is moved to the top left of the plot. Therefore, the area under the curve (AUC) should be large for a good classifier. The first results we present here use exactly these two quality measures to compare the DNN approach to the four named alternatives. All methods are applied to the synthetic data consisting of data based on mathematic formulas. Some data are available for 24 hours, while others span a time horizon of 48 hours and two separate neural networks are trained for these two settings.

<img src="https://user-images.githubusercontent.com/59834752/207903280-7218e305-117d-4387-af0d-af7630cfd79b.jpg" alt="ROC curves" width="245"/><img src="https://user-images.githubusercontent.com/59834752/207903419-5cf1eb5c-2e31-4459-92d0-fe79563e8175.jpg" alt="AUC curves" width="245"/><img src="https://user-images.githubusercontent.com/59834752/208038884-93f18918-5a85-4827-8b12-24a54ad02d2f.png" alt="AUC table" width="245"/>
*Figure/Table 3. Periodicity classification performance of different methods on synthetic data.* The left subfigure shows ROC curves for all compared methods and itself is divided into four subsets for four different data sets. The central subfigure shows the AUC of the ROC curves depicted on the left. The right table contains even more information, namely all AUC scores for synthetic data.

From the results depicted in Figure 3 it becomes clear that there is hardly any scenario, where DNNs as periodicity classifiers are outperformed. 
Besides experiments for synthetic data presented so far, the authors also evaluated their method on real-world data. Table 4 shows that DNNs perform very well also in this regime especially for the first two data sets. However, they are outperformed for the third depicted data set. 

<img src="https://user-images.githubusercontent.com/59834752/208039027-d2a483a1-c934-4a74-924d-e6cfdf05ea19.png" alt="real-world periodicity" width="480"/>

*Table 4. DNNs as binary periodicity classifiers perform best for 2 out of 3 data sets.* 

To obtain results for research question 2, the BioClock data set is divided into 70% training and 30% testing data. The BIO_CLOCK system is able to accurately predict the missing time of experiment with a mean absolute error of 75 minutes. In addition to this overall results obtained from all data, the authors divide the BioClock data set into several subsets corresponding to data from different tissues wild type mouse cells. Two of the four considered data subsets are created by using only brain and liver data, respectively. In addition, Set1 contains data from the adrenal gland, fat, gut, kidney, lung and muscle. Set 2 similarly agglomerates data from the aorta, colon, fibroblast, heart, macrophages and pituitary gland. Ideally, the measurement time prediction would become more reliable through this restriction to four homogeneous data sets. Similar to the first result regarding research question 1, the data are split into 70% training and 30% testing data.

Table 5 presents the mean absolute error of the measurement time prediction. Unsurprisingly, a classifier trained on one subset of data performs significatly worse when applied to data from different origins. However, a classifier trained on all data is always nearly as good or even better than a specialized DNN.

<img src="https://user-images.githubusercontent.com/59834752/208045508-b8d4f8dd-1c22-4eef-bd1a-1c510a3d9d78.png" alt="measurement time estimation" width="480"/>

*Table 5. DNNs perform well as estimators for measurement time.* 

## Conclusion

DNNs are able to answer both posed reasearch questions adequately: For time-series data like BioCycle, they can reliably predict periodicity as a boolean decision variable or quantitatively in terms of the period, lag and amplitude (results not shown here). For data without time measurement, the missing time can be reconstruced by the DNN system BIO_CLOCK. Unsurprisingly, both systems gain accuracy through the use of more data. 

