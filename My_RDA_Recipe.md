# Background
When I searched for the tools to detect the adaptation signitures, the SNPs probably associating to the adaptation, I found that some researchers using a method called 'redundancy analysis (RDA)' to identify the hiden association between the genomic data matirx and the environmental data, such as elevation and climatic data.  
This document will record my understanding regarding to the RDA technique.  

# Reference
The detailed information regarding RDA please check:  
**Numerical Ecology.3rd. Legendre, P. and Legendre, L. (2012).  Elsevier.**  

# 1. What is RDA (Redundancy analysis)?  
 - 1. RDA is one of the **canonical analysis** (Canonical analysis includes **asymmetric and symmetric canonical analysis**, and **RDA is a type of asymmetric canonical analysis**.). The canonical analysis is used to **perform the direct comparisons of two or more data table.** For example, the ecologists usually use this technique to investigate the relationship between a matrix describing species composition and a table of the environmental gradients of habitats.  
 - 2. Assuming we have two matriecs `Y` and `X`, and we want to find if the components of `Y` can be explained by `X` (a general formula will be `Y ~ X`). The basic idea of canonical analysis is to **force the ordination vectors of `Y` maximally related to the combinations of variables in `X`**.  
 - 3. Asymmetric canonical analysis combines the properties of ordination and regression, which **produces the ordinations of a response matrix `Y` that are constrainted to be maximally related to the linear combination of the explanatory variables `X`.**     
 - 4. Two commonly used asymmetric canonical analysis are RDA and CCA (canonical correspondence analysis). Both methods can be found in the R package `vegan`. The difference is that **RDA preserves the Euclidean distances** among objects in the matrix `Y-hat` (`Y-hat` is a linear combination of `X`), while the CCA preserves the Chi-square distances among objects in the matrix `Y-hat`.    
   
In sum, RDA is used when we **assume a response data matrix `Y` has a linear relationship with a explanatory data matirx `X`, and we want to investigate this relationship under the system of Euclidean distance**. If the `Y` matrix is a matrix of factors like the index matrix used in ANOVA, the the RDA is not a suitable method, and we need to switch to linear discriminant analysis (LDA). (I will not introduce LDA here)  

# 2. How RDA is done?
## Step1. multiple linear regression of `Y` on `X`
Assuming we have **a response data table `Y` which is a *n x p* matrix and a explanatory data table `X` which is a *n x m* matrix.** In the first step, the algorithm will **regress each variable of `Y` matrix (each column of `Y` represents a variable) on all variables of `X` matrix**. Then, we'll get the matrix of fitted values `Y-hat`.  
However, before performing the first step of RDA, we need the ensure our data meet two prerequisites:  
1. `Y` is dimentionally homogeneous. If not, we have to standardize `Y`.  
However, we should note that **the standardization is not appropriate if the meaning of `Y` will lose after standardization**, such as the species variance in a community. The homogeneity can determine whether the F test can be directly applied. But, if the our `Y` is not homogeneous **we can still conduct a permutation test to examine the significance of relationship between `Y` and `X`**, so the homogeneity is actually not a matter.   
2. ***The variables of `X` should not be collinear with each other.*** If the problem with collinearity exists, it will make the inference of multiple regression become unstable, so we need to discard some variables.  
 - **Tip**: The standardized `X` has no effect on the result of RDA, but it could be good to standardize `X` for the convenience of programming (Legendre, P. and Legendre, L. 2012. ***p.630***).
### How to handle collinearity of variables in `X`?
The solution of collinearity is introduced in the **pages 557 - 559 (Numerical Ecology.3rd. Legendre, P. and Legendre, L. 2012**). In brief, the authors recommended to 
 - 1. **ordering the variables based on their importance**, such as placing the ecological informative or easy-to-measure variable first. 
 - 2. **computing the sigular value decomposition (SVD) sequentially using the first *n* columns and *n+1* columns.** If we find the sigular value is 0 when adding a new variable, then it means the new variable is collinear with the previous variables, so we should discard the new variable.
 - 3. **calculating variance inflation factors (VIFs) for each variable (Legendre, P. and Legendre, L. 2012. *p.558* Equation 10.17).** The VIF of *j*th variable in the `X` matrix is calculated based on the `R^2` obtained by regressiong *j*th variable on all the other variables in `X` matrix. If the VIF of a specific variable is too high, then it should be considered as the candidate to remove. The commonly used cut-off of VIF is >5, >10, and >20. The VIF can be computed by using the `vif()` function in the R package `car`.
 
 ### Test the significance of the relationship between `Y` and `X`
 After performing the multiple regression, we should first make sure the relationship of two data table is significant. Otherwise, it is meaningless to carry out further analysis. According to the **page 632-634 of *Numerical Ecology.3rd. (Legendre, P. and Legendre, L. 2012*)**, the `R^2 = SS(Y-hat)/SS(Y)` can be computed and the F test can then conduct to test if the `R^2` is significant or not. However, this is for the situation that the `Y` is homogeneous.  
 - **When `Y` is not homogeneous, we should use the permutation test.**  
 - The permutation test for RDA is available in the `rda()` function in the `vegan` package.
 - **Null hypothesis of the test:**  
 **The linear relationship is not larger than the relationship between the unrelated `Y` and `X` matrics of the same size (Legendre, P. and Legendre, L. 2012. *p.633*).** 
 
 ## Step2. Perform PCA on the fitted value matrix `Y-hat`
 After ordination, we may be interested in how many canonical axes can used to explain the linear dependence of `Y` and `X`. We can test the significance of each canonical axis using the `permutest.cca()` function in the `vegan` package.  
Suppose we are testing the *j* th axis. The null hypothesis of the test is **'the linear dependence of the response data `Y` and the explanatory data `X` is less than *j* dimension'** (see Legendre, P. and Legendre, L. 2012. *p.634 - 635* ). 

 

# 3. How to correct population structure?




## What is Moran's I ?
Moran's I is a correlation coefficient used to measure the degree of spatial autocorrelation. In brief, **it describes how objects are similar or dissimilar with the objects surrounding them.** It can be **any value between -1 and 1**. 
 - ***If Moran's I is -1, it indicates the observed objects are in 'perfect dispersion' with their neighbors, which means all the nearby objects are dissimilar with the given object.***   
 - In contrast, ***when Moran's I is 1, it indicates the objects are in 'perfect clustering'.***   
 - ***If Moran's I is equal to 0 means completely random spatial pattern.***  
(More details, please check: https://www.statisticshowto.datasciencecentral.com/morans-i/)  
  
Since Moran's I is a correlation coefficient, we can use it to do statistical test to understand if the observed data is randomly distributed or it has some spatial pattern. **The null hypothesis for this test is 'the data is randomly distributed'** (For the R tutorial, please check: https://cran.r-project.org/web/packages/adespatial/vignettes/tutorial.html)

## What is Moran's eigenvector maps (MEM)?
MEM is 

## Problem with the correction based on MEM
Here is the E-mail from Dr. Brenna R. Forester, who proposed the method correcting population structure in RDA by using MEM ([Forester et al. 2018](https://onlinelibrary.wiley.com/doi/full/10.1111/mec.14584)):  
> Hi Che-Wei,  
>  
> Thanks for your interest in our paper. I apologize that the supplement is not available online - I've repeatedly requested that the journal add it, but they have yet to do so.    
>    
> I've attached it here. However, please note that ***my recent (still unpublished) work has indicated that MEMs are a very conservative approach to correcting for population structure in RDA*** - and that ***using PCs uncorrelated with your environmental predictors may be a better way to proceed.***    
>  
> If you do want to use MEMs, I would not necessarily recommend using the MEM calculation approach we used in the paper - it may work well for your data set and sampling design, but ***customizing the MEM approach based on your data set is the best approach. See this recent paper on optimizing the spatial weighting matrix (attached) with excellent supplementary tutorial (with R code, also attached) to use some newer approaches to choosing the best MEM selection approach.*** For example, with clustered sampling designs, I find that the PCNM method for MEMs works best at finding the largest scale spatial eigenvectors.    
>    
> Best,  
> Brenna  
  
According to Dr. Forester's suggestion , the MEM approach used in their previous study is very conservative, and she would recommend:    
**1. customizing the spatial weighting matrix used for MEM approach.**  
**2. using PCs uncorrelated to environmental variables is another good option.**   


# 4. What is partial RDA (Legendre, P. and Legendre, L. 2012. page 649 - 658)?
In brief, partial RDA attempts to explain the response variables `Y` by using the explanatory variables `X` with the given effect of covariables `W`. To understand the partial RDA, we have to first understand what is the partial regression.

## (1) Partial regression (Legendre, P. and Legendre, L. 2012. page 570)
Suppose we have *two explanatory datasets, and there are correlatins among them*. In this situation, we may want to **estimate the amount of variation that is exlusively attributed to one of the dataset which we are interested in**. Thus, we would like to take the effect of the correlated dataset into account and control for it when fitting the model for our target dataset.  
### Process of partial regression
Assume we have a vector of the response variable, called `y`, a matrix of the explanatory variables `X`, and a matrix of covariables `W`. The partial regression coefficients can be obtained by the following steps:  
 - 1. regress `y` on `W` to get the residuals `y-res|W`, and regress `X` on `W` to get residuals `X-res|W`.  
 - 2. regress `y` on `X-res|W` or regress `y-res|W` on `X-res|W`. (Two methods will generate the identical partial regression coefficients but different intercept.)  
 
## (2) Process of partial RDA
Similarly, assume we have response variables `Y`, explanatory variables `X`, and covariables `W`. Then, the partial RDA will be done by:  
 - 1. regress `Y` on `W` to get the residuals `Y-res|W`, and regress `X` on `W` to get residuals `X-res|W`.  
 - 2. regress `Y` on `X-res|W` or regress `Y-res|W` on `X-res|W`.  
 - 3. perform PCA   
 
 The RDA of `Y` by `X-res|W` and the RDA of `Y-res|W` by `X-res|W` have the same eigenvalues, eigenvectors, and canonical axes. In `vegan` package, the RDA is conducted based on the approach of `Y-res|W` with `X-res|W`.
 
## (3) Test of significance in partial RDA 
 Like simple RDA, we would like to know if the linear relationship between `Y` and `X` is significant or not. In the `vegan` package, `permutest.cca()` provides three types of permutation test (Legendre, P. and Legendre, L. 2012. page 652):  
  - 1. permuting the rows of `Y` (with the argument `method = "direct"`)  
  - 2. permuting the rows of `Y-res|W` (with the argument `method = "reduced"`)  
  - 3. fitting the full-model `Y ~ X + W` to obtain `Y-fit|XW` and `Y-res|XW`, and then permuting the rows of `Y-res|XW` generating permuted residuals `Y*-res|XW`. Finally the permuted `Y*` is obtained by adding `Y-fit|XW` to `Y*-res|XW`. 
  - **NOTE**: permutation test is not suitable if the covariables containing outliers.
  
 




# How to interpret the biplot of RDA?

# Memo:
 - second RDA with only outliers
