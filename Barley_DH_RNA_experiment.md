# Introduction
This `markdown` file is used to record the RNA experiment. 

# Cost
## Cost of RNA extraction
- According to the discussion with Sonja on 12.03.2020, she said the cost of RNA extraction per sample could be around 40 Euro to the best of her knowledge (I guess she combined the cost of extraction and library construction).  
- [Digel et al. (2015)](https://doi.org/10.1105/tpc.15.00203) (cited by [Weisweiler et al. (2019)](https://doi.org/10.1186/s12864-019-6174-3)) used RNeasy Micro Kit (Qiagen) and TRIzol (Life Technologies) to extract RNA.   
           - a. The [RNeasy Micro Kit](https://www.qiagen.com/de/products/discovery-and-translational-research/dna-rna-purification/rna-purification/total-rna/rneasy-micro-kit/?clear=true#orderinginformation) costs 508 Euro for 50 preps -> **in average 11 Euro per sample**.   
           - b. The [TRIzol](https://www.thermofisher.com/order/catalog/product/15596026#/15596026) costs 262 and 381 Euro for 100 ml and 200 ml, respectively. 100 ml of TRIzol can used for 100 preps     
      -> **the average cost would be 1.9 Euro** if using 200 ml reagent. (But other reagents are required for TRIzol method. See the table 2 of the [TRIzol user guide](http://tools.thermofisher.com/content/sfs/manuals/trizol_reagent.pdf))  
      -> Prof. Benjamin Stich replied my email on 17.03.2020, and **he said they used [RNeasy Micro Kit](https://www.qiagen.com/de/products/discovery-and-translational-research/dna-rna-purification/rna-purification/total-rna/rneasy-micro-kit/?clear=true#orderinginformation) in their study.**   

- [Pallares et al. 2020](https://www.g3journal.org/content/10/1/143) developed an RNA extraction protocol based on using **[Dynabeads mRNA DIRECT Purification Kit](https://www.thermofisher.com/order/catalog/product/61012#/61012)**, and they reduce the cost to around 1.7 USD per sample. However, this cost was calculated from the method designed for Drosophila, which required 20 micro litter of beads (See [File S2 of Pallares et al. 2020](https://gsajournals.figshare.com/articles/Supplemental_Material_for_Pallares_Picard_and_Ayroles_2020/9905279)). Since our sample is much larger, more beads may needed to collect more RNA.   
The cost of [Dynabeads mRNA DIRECT Purification Kit](https://www.thermofisher.com/order/catalog/product/61012#/61012) is 954 Euro for 10 ml, which can be used for 500 preps if following the protocol of [Pallares et al. 2020](https://www.g3journal.org/content/10/1/143). -> **the average cost per sample is 1.9 Euro... (NOT including other reagents)**  
  
As cost per sample for the methods mentions above is around 2 Euro just for reagent, I think we could to estimate the cost for RNA extraction to be ranging from 4 to 6 Euro per sample.

## Cost of RNA library construction
According [Pallares et al. 2020](https://www.g3journal.org/content/10/1/143), the TM3'-seq method cost 1.5 USD per sample for the reagent. I would like to estimate it to be 2 Euro.

## Cost of RNA sequencing
If we use the 20 milion reads with 2 x 150 bp like [Weisweiler et al. (2019)](https://doi.org/10.1186/s12864-019-6174-3), **the cost would be 60 Euro per sample (10 Euro per Gb)**.


# Pre-trial
## First trial
### 1. Timeline
- Start: 2020-03-13
- Seed germination in the growth chamber with 16 hours of light and 8 hours of darkness under 22&deg;C (from 2020-03-13 to 2020-03-18) 
- End: 2020-03-18 (original plan is to end on 2020-03-20. However, due to the coronavirus, which made things complex and we cannot get liquid nitrogen as our plan, we terminated the trial earlier.)
### 2. Objective
- check the growth of seedlings
- check the feasibility of our experiment system, including sterilization, sowing seeds, harvesting

### 3. 



# Growth condition of seedlings
## Issue
- (1) When should we harvest seedlings?  
-> [Weisweiler et al. (2019)](https://doi.org/10.1186/s12864-019-6174-3) collected
(EDITING)


# RNA extraction
[Weisweiler et al. (2019)](https://doi.org/10.1186/s12864-019-6174-3) cited the work of [Digel et al. (2015)](https://doi.org/10.1105/tpc.15.00203) for the details of RNA extraction. Here is the description of [Digel et al. (2015)](https://doi.org/10.1105/tpc.15.00203): 
> The samples harvested for RNA extraction were frozen immediately in liquid nitrogen and stored at −80°C. Total RNA, excluding miRNAs, was extracted from ground tissue using an **RNeasy Micro Kit (Qiagen) and TRIzol (Life Technologies) for RNA sequencing and qRT-PCR, respectively**. Residual DNA was removed using a **DNA-free kit (Ambion).** RNA extraction and DNase treatment were performed according to the manufacturer’s instructions. The RNA concentration and integrity were determined using a 2100 Bioanalyzer (Agilent) before RNA library preparation for RNA sequencing. Owing to the column-based RNA purification method of the RNeasy Micro Kit, only transcript species larger than 200 nucleotides were further processed for RNA sequencing.  


# RNA sequencing
## Sequence depth
According to [Weisweiler et al. (2019)](https://doi.org/10.1186/s12864-019-6174-3), they had around 20 million 2x150 bp reads for one sample. Their finding suggested using 1% \~ 5% of reads can still obtain acceptable prediction ability. 
  
In their article, the authors mentioned that the cost of 20 million 2x150 bp reads is 60 Euro and the library construction is 2 Euro per sample if using the latest protocol (BRB-seq; [Alpern et al. 2019](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-019-1671-x)). (According to [Pallares et al. 2020](https://www.g3journal.org/content/ggg/10/1/143.full.pdf), the commercial RNA kits cost 35 USD \~ 44 USD per sample.)   

> However, the cost of genotyping one sample with the barley 50K SNParray is with about 50 Euro \[42] also less than the mRNA sequencing analysis. When generating it newly with latest protocols and sequencing chemistry one could expect that the mRNA sequencing of **one sample would cost about 2 Euro for the mRNA library preparation \[43] as well as 60 Euro for 20 million 2x150 bp reads**.  

If we calculate the cost according to this number, the total cost will be `(800 + 15 parents * 3 batches) * 62 = 52390 Euro`. This is definitely not possible to spend so much money on sequencing. So, we should use other methods for sequencing RNA.
  
If we take the authors suggestion reducing the read number to 2 million 2x150 bp reads (10% * 20 million 2x150 bp) the cost per sample will be `(800 + 15*3) * [(60 * 0.1) + 2] = 6760 Euro` which is more affordable.
## RNA library
We currently have two new methods for preparing RNA library.
- TM3'seq: [Pallares et al. 2020](https://www.g3journal.org/content/ggg/10/1/143.full.pdf) -> We will use this one
- BRB-seq: [Alpern et al. 2019](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-019-1671-x)
