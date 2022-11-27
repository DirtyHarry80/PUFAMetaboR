#### Set working directory ----
setwd("/Your/Favourite/Directory")

#### Launch necessary packages ----
library(MetaboAnalystR)
library(outliers)

# Create the mSet object
mSet<-InitDataObjects(data.type = "pktable",anal.type = "stat",FALSE)
mSet<-Read.TextData(mSet,"ExampleData-PUFA-MYOF.txt", "colu", "disc")
mSet<-SanityCheckData(mSet)

# Replace missing values
mSet<-ReplaceMin(mSet)

# Filtering and Normalization
mSet<-FilterVariable(mSet, "iqr", "F", 25)
mSet<-PreparePrenormData(mSet)
mSet<-Normalization(mSet, "QuantileNorm", "NULL", "AutoNorm", ratio=FALSE, ratioNum=20)

mSet <- PlotNormSummary(mSet, "norm_0_", "png", 600, width=NA)
mSet <- PlotSampleNormSummary(mSet, "snorm_0_", "png", 600, width=NA)

# Test for outliers
md.matrix <- as.matrix(mSet[["dataSet"]][["norm"]]) 
outlier <- apply(md.matrix[1:5,],2,grubbs.test) #replace [1:5,] by [6:10,] to test for shMYOF
outlier.1 <- sapply(outlier,function(x) x$p.value)
outlier.2 <- sapply(strsplit(names(outlier.1),split = ".",fixed = "T"),function(x) x[2])
outlier.3 <- table(outlier.2[outlier.1<0.05]) #the lower the value the least chance is outlier
outlier.3
# In our example shNT4 is the outlier

# Remove the outlier condition in the normalized data
# Removing shNT4, hence remove the 4th row in the data frames and vectors
mSet[["dataSet"]][["norm"]] <- mSet[["dataSet"]][["norm"]][-4,] 
mSet[["dataSet"]][["row.norm"]] <- mSet[["dataSet"]][["row.norm"]][-4,]
mSet[["dataSet"]][["prenorm"]] <- mSet[["dataSet"]][["prenorm"]][-4,]
mSet[["dataSet"]][["filt"]] <- mSet[["dataSet"]][["filt"]][-4,]
mSet[["dataSet"]][["proc"]] <- mSet[["dataSet"]][["proc"]][-4,]
mSet[["dataSet"]][["preproc"]] <- mSet[["dataSet"]][["preproc"]][-4,]
mSet[["dataSet"]][["orig"]] <- mSet[["dataSet"]][["orig"]][-4,]
mSet[["dataSet"]][["cls"]] <- mSet[["dataSet"]][["cls"]][-4]
mSet[["dataSet"]][["orig.cls"]] <- mSet[["dataSet"]][["orig.cls"]][-4]

# Perform PCA
mSet <- PCA.Anal(mSet)
mSet <- PlotPCAPairSummary(mSet, "pca_pair_0_", "png", 600, width=NA, 5)
mSet <- PlotPCAScree(mSet, "pca_scree_0_", "png", 600, width=NA, 5)
mSet <- PlotPCA2DScore(mSet, "pca_score2d_0_", "png", 600, width=NA, 1,2,0.95,1,0)
mSet <- PlotPCALoading(mSet, "pca_loading_0_", "png", 600, width=NA, 1,2);
mSet <- PlotPCABiplot(mSet, "pca_biplot_0_", "png", 600, width=NA, 1,2)
mSet <- PlotPCA3DScoreImg(mSet, "pca_score3d_0_", "png", 600, width=NA, 1,2,3, 40)

# Partial Least Square Analysis
mSet<-PLSR.Anal(mSet, reg=TRUE)
mSet<-PlotPLSPairSummary(mSet, "pls_pair_0_", "png", 600, width=NA, 5)
mSet<-PlotPLS2DScore(mSet, "pls_score2d_0_", "png", 600, width=NA, 1,2,0.95,1,0)

# Volcano Plot
mSet <- Volcano.Anal(mSet, FALSE, 2.0, 0, 0.75,F, 0.1, TRUE, "raw")
mSet <- PlotVolcano(mSet, "volcano_0_",1, "png", 600, width=NA)

# Heat Map
mSet<-PlotHeatMap(mSet, "heatmap_0_", "png", 600, width=NA, "norm", "row", "manhattan", "ward.D","bwm", "overview", T, T, NA, T, F)

# Dendogram
mSet<-PlotHCTree(mSet, "tree_0_", "png", 600, width=NA, "kendall", "ward.D")

# Correlation & Feature Corr.
mSet<-PlotCorrHeatMap(mSet, "corr_0_", "png", 600, width=NA, "col", "kendall", "bwm", "overview", F, F, F, 100, "0")
mSet<-FeatureCorrelation(mSet, "kendall", "9-HETE")
mSet<-PlotCorr(mSet, "ptn_1_", "png", 600, width=NA)
