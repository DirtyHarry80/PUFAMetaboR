# PUFAMetaboR

A script based on MetaboAnalystR (https://www.metaboanalyst.ca/home.xhtml) to analyse metabolomics data from targeted analysis of poly-unsatturated fatty acids. The objective is to present a condensed version with minimum necessary features, enabling the creation of standard plots (e.g. heatmap, correlation matrix, etc.). The script contains also a possibility to test for and remove outliers, beased on Grubbs test and Outliers package (https://cran.r-project.org/web/packages/outliers/outliers.pdf).

A test dataset is included based on PUFA analysis of breast tumors silenced for MYOF gene (shMYOF) and corresponding negative controls (shNT). One analysis of these raw data has originally been published in PMID: 27775075.

For further practical details, including protocol for sample measurement, refer to Turtoi E et al. STAR Protocols 2022. 

N.B.: Installation of specific R Packages (e.g. MetaboAnalystR & Outliers) is required before using the script; See the "Libraries" section of the script. 
