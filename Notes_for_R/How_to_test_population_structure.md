# Background
When studying population structure, we may want to test the significance of the population structure. To do this we can use the permutation test provided in ***hierfstat*** package.  
Details are in the note of the package:  
https://www2.unil.ch/popgen/softwares/hierfstat.pdf  
  
# Permutation test
Here I just briefly introduce the concept how the populations are premuted.  
Assuming we have 
- 3 populations: A1, A2, A3  
- Each population has 10 subpopulation: Bi1, Bi2 ..., Bi10  
- Each subpopulation has 100 individuals: Cij1, ..., Cij100  
1. Then, to test the structure among "A", the subpopulations "B" will be permuted among "A" but the individuals "Cij" within corresponding "Bij" will be fixed as the units for permutation when permuting.  
2. Similarly, to test the structure among "B", the individuals "Cij" will be permuted among "Bij", but the permutation will be only performed within "Ai". For example, Cijk will not permute with C(i+1)jk
