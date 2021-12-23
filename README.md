---
title: |
  | Prediction of Absenteeism 
subtitle: (CSE780 project)
author: Paria Fakhrzad - Student ID 400353290 \hspace{10in} Program of Computational Science and Engineering \hspace{10in}  McMaster University 
date: "12/01/2021"
output: 
  beamer_presentation:
    theme: "Madrid"
    colortheme: "beaver"
    fonttheme: "Default"
    slide_level: 2
    includes:
      in_header: header.tex
fontsize: 12pt
bibliography: Project.bib
nocite: | 
---
```{r}
library(dplyr)
library(Hmisc)
library(magrittr)
library(readr)
library(ggplot2)
library(ISLR2)
library(class)
library(ggpubr)
library(corrplot)
library(GGally)
library(PreProcess)
library(caTools)
library(caret)
library(GGally)
library(PreProcess)
library(tree)         #tree/CART
library(MASS)
library(mclust)       #Gaussian Mixtures
library(car)
library(boot)         #CV
library(e1071)
library(leaps)
library(glmnet)
library(pls)
library(gridExtra)
library(mgcv)         #GAM
library(randomForest) #Random Forest

## Outline
 - Data exploration
 - Regression methods
 - Classification methods
 - Results
 - Discussion
 

\tiny 
### Code and Resources used
\tiny
 R version : 4.0.5
 Packages: dplyr, readr, ggplot2, class, randomForest[@r], boot, tree
 Dataset[@UCI]

 
## Motivation 
In following study we are going to address to one of the important workplace challenges that is absenteeism[@Kocakulah2016]. our aim is:

 - Focus on this as a measurable problem
 
 - Detect the relationship between predictors and response 
 
 - Build prediction models to predict Absenteeism time in Hours
 
 - Fit classification models to classify whether it is long or short absence

 
## Data 
Dataset is related to 740 records of absenteeism at work for three years (July 2007-July 2010) in a courier company in Brazil [^1]

  - There are 20 features/predictors in this dataset- without `NA`
  - The response/label is one continues column (hour)
  - `46%`of observations have absence hour more that median


\tiny
```{r, results='asis',echo=FALSE}
knitr::kable(head(Absence_df[,1:11]),caption = "Sample of Dataset",align=c("c","c","c","c","c","c","c","c","c","c"))
knitr::kable(head(Absence_df[,12:21]),align=c("c","c","c","c","c","c","c","c","c","c"))
```
[^1]:\tiny[\textit{UCI Machine Learning Repository}](http://archive.ics.uci.edu/ml/datasets/Absenteeism+at+work#)


## Data exploration by visualization

 - There are 28 Reasons that 23, 28, 27 and 13 have most count of absence in observations that are (medical and dental consultation, physiotherapy, musculeskeletal disorders)
 - Reasons 13,19 and 22 have the most long absence that need more investigation 
 - Height, weight and body_mass have a high collinearity based on correlation matrix


\tiny
![count of Absence reason](figure4.png){width=50%}|![count of Absence reason](figure5.png){width=50%}


## Methods- Classification

Target: finding the class of absence time length
 
 - Logistic Regression:
    - Best subset used for feature selection
    - confusion matrix for accuracy test accuracy is `77%`
    - K-fold CV applied with K=7
      
 - Classification tree
    - test accuracy `80.9%`
    - Pruning with optimal node 10 and`81.5%`+interpretable

\tiny    
![K-fold](plotcv.png){width=50%}|![Tree](Tree.png){width=40%}

```{r results='asis',echo=FALSE}
#grid.arrange(graph2, graph3, ncol = 1)
```
## Methods- Regression

Target: predicting the absence hours

- Multiple linear regression
     - $R^2=0.2$ and $RMSE=10.8$ $MAE=5.53$
     
   
- Regression tree
     - Number of terminal nodes is 16
     -  $R^2=0.07$ and $RMSE=14.62$ $MAE=6.38$

\tiny
![](regression.png){width=100%}|

## Results 

### In classification part for binary response variable:
 
 - The accuracy of regression tree is more than logistic regression
 - We applied LDA and Random forest and both have less accuracy
 - Because of high correlation between variables
 - VIF shows multicollinearity in body_mass, height, weight
 
### In Regression part for continuous response variable:
 
 - We are usign MAE and RMSE to compare models
 - The linear regression works better in this part
 


## Discussion 
- In regression part there is challenge for having huge number of feature
- Possible improvement by focusing more on feature selection
- Since the response label in balanced the stratification of data is not important

##

  \begin{center}
			\textbf{{\LARGE Thank You!}}
		\end{center}
		

## References 
