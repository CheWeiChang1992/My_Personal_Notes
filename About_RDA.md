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
 - 4. 
 
