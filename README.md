# ClusterAEA2019
---
title: "Cluster"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

Load in data
```{r}
setwd("S:/Indiana Research & Evaluation/Matthew Hanauer/AEA2019")
cluster_data = read.csv("Demographics by location.csv", header = TRUE)
```
Look at data
```{r}
head(cluster_data)
describe(cluster_data)
head(cluster_data)
cluster_data_sub = data.frame(female = cluster_data$Female.N, white = cluster_data$White.or.Caucasian.N, average_age = cluster_data$Average.Age)
describe(cluster_data_sub)
```
Try cluster
```{r}
library(cluster)
library(factoextra)
gower_dis = daisy(cluster_data_sub, metric = "gower")
gower_dis

anges_dat = agnes(x = gower_dis, diss = TRUE, method = "ward")
hcTree = cutree(anges_dat, k=3)
cluster_data_sub$hcTree = hcTree
cluster_data$hcTree = hcTree
cluster_data
cluster_data_sub
cluster_map = fviz_cluster(list(data =cluster_data_sub, cluster = hcTree, repel = TRUE))
cluster_map
cluster_data_sub



```

