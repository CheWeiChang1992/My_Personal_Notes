# Experiment design


# Growing seedlings



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
