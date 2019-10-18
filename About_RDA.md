# Background
When I searched for the tools to detect the adaptation signitures, the SNPs probably associating to the adaptation, I found that some researchers using a method called 'redundancy analysis (RDA)' to identify the hiden association between the genomic data matirx and the environmental data, such as elevation and climatic data.  
This document will record my understanding regarding to the RDA technique.  

# Reference
The detailed information regarding RDA please check:  
**Numerical Ecology.3rd. Legendre, P. and Legendre, L. (2012).  Elsevier.**

# What is RDA (Redundancy analysis)?  
 - 1. RDA is one of the **canonical analysis** (Canonical analysis includes **asymmetric and symmetric canonical analysis**, and **RDA is a type of asymmetric canonical analysis**.). The canonical analysis is used to **perform the direct comparisons of two or more data table.** For example, the ecologists usually use this technique to investigate the relationship between a matrix describing species composition and a table of the environmental gradients of habitats.  
 - 2. Assuming we have two matriecs `Y` and `X`, and we want to find if the components of `Y` can be explained by `X` (a general formula will be `Y ~ X`). The basic idea of canonical analysis is to **force the ordination vectors of `Y` maximally related to the combinations of variables in `X`**.  
 - 3. Asymmetric canonical analysis combines the properties of ordination and regression, which **produces the ordinations of a response matrix `Y` that are constrainted to be maximally related to the linear combination of the explanatory variables `X`.**     
 - 4. Two commonly used asymmetric canonical analysis are RDA and CCA (canonical correspondence analysis). Both methods can be found in the R package `vegan`. The difference is that **RDA preserves the Euclidean distances** among objects in the matrix `Y-hat` (`Y-hat` is a linear combination of `X`), while the CCA preserves the Chi-square distances among objects in the matrix `Y-hat`.    
   
In sum, RDA is used when we **assume a response data matrix `Y` has a linear relationship with a explaintory data matirx `X`, and we want to investigate this relationship under the system of Euclidean distance**. If the `Y` matrix is a matrix of factors like the index matrix used in ANOVA, the the RDA is not a suitable method, and we need to switch to linear discriminant analysis (LDA). (I will not introduce LDA here)  

# How RDA is done?
## Step1. multiple linear regression
Assuming we have **a response data table `Y` which is a *n x p* matrix and a explaintory data table `X` which is a *n x m* matrix.** In the first step, the algorithm will **regress each variable of `Y` matrix (each column of `Y` represents a variable) on all variables of `X` matrix**. Then, we'll get the matrix of fitted values `Y-hat`.  
However, before performing the first step of RDA, we need the ensure our data meet two prerequisites:  
1. `Y` is dimentionally homogeneous. If not, we have to standardize `Y`.  
However, we should note that **the standardization is not appropriate if the meaning of `Y` will lose after standardization**, such as the species variance in a community. The homogeneity can determine whether the F test can be directly applied. But, if the our `Y` is not homogeneous **we can still conduct a permutation test to examine the significance of relationship between `Y` and `X`**, so the homogeneity is actually not a matter.   
2. ***The variables of `X` should not be collinear with each other.*** If the problem with collinearity exists, it will make the inference of multiple regression become unstable, so we need to discard some variables.  

### How to handle collinearity of variables in `X`?
The solution of collinearity is introduced in the **pages 557 - 559 (Numerical Ecology.3rd. Legendre, P. and Legendre, L. 2012**). In brief, the authors recommended to 
 - 1. **ordering the variables based on their importance**, such as placing the ecological informative or easy-to-measure variable first. 
 - 2. **computing the sigular value decomposition (SVD) sequentially using the first *n* columns and *n+1* columns.** If we find the sigular value is 0 when adding a new variable, then it means the new variable is collinear with the previous variables, so we should discard the new variable.
 - 3. **calculating variance inflation factors (VIFs) for each variable.** If the VIF of a specific variable is too high, then it should be considered as the candidate to remove. The commonly used cut-off of VIF is >5, >10, and >20.
 
 ### Test the significance of the relationship between `Y` and `X`
 After performing the multiple regression, we should first make sure the relationship of two data table is significant. Otherwise, it is meaningless to carry out further analysis. According to the **page 632-634 of *Numerical Ecology.3rd. (Legendre, P. and Legendre, L. 2012*)**, the `R^2 = SS(Y-hat)/SS(Y)` can be computed and the F test can then conduct to test if the `R^2` is significant or not. However, this is for the situation that the `Y` is homogeneous.  
 - **When `Y` is not homogeneous, we should use the permutation test.**  
 - The permutation test for RDA is available in the `rda()` function in the `vegan` package.
 - **Null hypothesis of the test: The linear relationship is not larger than the relationship between the unrelated `Y` and `X` matrics of the same size.** 
 
 ## Step2. Perform PCA on the fitted value matrix `Y-hat`
 

 
# What is partial RDA?

# How to correct population structure?
