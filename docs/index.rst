======
HiCRep
======

HiCRep is a python implementation of the R package with the same name. It provides a tool for assessing the reproducibility of Hi-C datasets based on the algorithm published by `Yang et al. <https://pubmed.ncbi.nlm.nih.gov/28855260/>`_
In brief, data is first smoothed to reduce the effects of noise and bias and then stratified by contact distance to adjust for the distance dependency of Hi-C datasets. These strata are compared between samples to calculate the stratum-adjusted correlation coefficient (SCC). The SCC is a value between -1 and 1 and can be interpreted the same way you would a standard correlation. 


This implementation takes a pair of Hi-C data sets in Cooler format (.cool for single binsize or .mcool formultiple binsizes) and computes the HiCRep SCC scores for each pair of chromosomes between the two data sets. It can be run either as a command line tool of through a python API. 

Installation
============
HiCRep req

numpy
scipy
cooler

we recommend using pip to install hicrep, which will install missing dependencies automatically. 

API
===



CLI
===
