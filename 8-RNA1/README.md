# Test Yourself

1. In which of the following cases poly-A selection should not be used during RNA-seq library prep?
* You are interested in the abundance of various tRNA molecules
* You want to include mitochondrial genes in a differential gene expression analysis
* The sample contains lots of pre-mRNA
* You only want to sequence the 5’ ends of transcripts
* You work on bacteria

2. You perform an RNA-Seq experiment and analysis and find that there are 100 reads corresponding to gene X and 170 reads corresponding to gene Y. The transcript length for X and Y are 2000 bp and 1800 bp, respectively. Which gene shows higher expression level?
* Gene X
* Gene Y
* Same level
* Impossible to tell without the total number of reads in the experiment

3. Which of the following biological questions cannot be answered using a differential gene expression analysis?
* Which of the human genes undergo RNA editing?
* How does E. coli respond to high salinity medium?
* When deleting the gene CHA1 from the yeast genome, how does the expression of the rest of the genes change?
* What genes are expressed in human epithelial lung cells when they are infected with COV-SARS-2?

4. In which of the following cases we must use a splice-aware mapping tool (`STAR`) and not a regular tool (`BWA`)?
* Mapping RNA-seq reads to an eukaryotic reference genome 
* Mapping RNA-seq reads to an eukaryotic reference transcriptome
* Mapping RNA-seq reads to a prokaryotic reference genome 
* Mapping RNA-seq reads to a prokaryotic reference transcriptome

5. You map RNA-seq reads to a reference genome and run `Qualimap` on the resulting mapping. To your horror, you see that only about 30% of the reads map to exonic regions. What could have caused that?
* mRNA was not enriched properly during library prep
* The genome annotation is taken from a strain too different from the strain that was sequenced
* Not enough reads were generated
* There is a bias towards reads originating from the 3’ end of transcripts

