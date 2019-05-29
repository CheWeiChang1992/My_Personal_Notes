# Background
There are several way to do PCA in R. Therefore, I am interesting in whether they produce the identical results or not. (In theory, they should be...)  
For this reason, I try to perform PCA to understand how to get the same PC plot using four different R function.

# R codes
For the convenience, I used our unpublished genomic data, which including 281 samples and 9k SNPs  
1. prepare data  
`library(vcfR)`  
`vcf = extract.gt(read.vcfR(args.in$vcf)) # read the vcf file`  
`numvcf <- ifelse(as.matrix(vcf) == '0/0',0,1) # convert to numeric data`  
`numvcf <- apply(numvcf,1, function(x){x[is.na(x)] <- mean(x, na.rm = T);return(x)}) # impute missing value using mean`  
  
2. Perform PCA using different functions  
`svdtest <- svd(apply(numvcf,2,function(x){x-mean(x)}))`  
`pctest = prcomp(numvcf)`  
`pc2test = princomp(cor(t(numvcf)))`  
`eigentest <- eigen(cor(t(apply(numvcf,2,function(x){x-mean(x)}))))`  

3. Draw the figure  
`par(mfrow = c(2,2))`
`plot(pctest$x[,1],pctest$x[,2], main = "prcomp")`
`plot(svdtest$u[,1],svdtest$u[,2], main = "svd")`
`plot(pc2test$scores[,1],pc2test$scores[,2], main = "princomp")`
`plot(eigentest$vectors[,1],eigentest$vectors[,2], main = "eigen")`
  
Even though the values of projection are not identical, the pattern is very consistent. So it should be no problem for me to analyze population structure.  
![PCAtest](https://github.com/CheWeiChang1992/My_Personal_Notes/blob/master/Figures/PCAtest.png)

# Tips
1. Be aware of the dimension of the data. The samples or observations should be ordered by row.  
2. When using 'svd' and 'eigen' function, we have to center the data.  
3. When using 'princomp' and 'eigen', we need to use the correlation matrix as the input.  
