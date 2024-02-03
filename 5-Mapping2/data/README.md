# Test Yourself

1. In which of the following cases would you choose to use BWA?
* Mapping reads of a heat-resistant Arabidopsis thaliana strain to the reference genome in order to detect sequence variation.
* Mapping RNA-seq reads of yeast to the reference genome to find which genes express higher under stress conditions.
* Searching a database of bacterial genes for a whole gene sequence isolated from a soil sample.
* Mapping reads sequenced from chicken to the mouse genome in order to estimate their genetic distance.


2. Which of the following SAM flags described a mapped read?
* 99
* 0
* 16
* 149
* 4

3. What can you say about the following SAM record?

![SAM record](sam.example.png)

* This read comes from a paired-end library
* This read probably has an equally-good mapping in another location
* The other read in the pair was mapped to ChrXII
* The probability that the mapping position is correct is larger than 99.99%
* The read got a low mapping quality score because its paired read is unmapped

4. What `samtools` command/s will convert a `SAM` file to a `BAM` file that only contains reads with ```MAPQ > 30``` and mapped to `Chr3`?
* 
```bash
samtools view -bh -q 30 aln.sam Chr3 > filter.bam
```
* 
```bash
samtools view -bh -q 30 aln.sam Chr3 -o filter.bam
```
* 
```bash
samtools view -H -q 30 aln.sam Chr3 > filter.bam
```
* 
```bash
samtools view -bh -q 30 -F 4 aln.sam > filter.bam
```
* 
```bash
samtools view -bh -q 30 -c Chr3 aln.sam > filter.bam
```
* 
```bash
samtools view -H -q 30 aln.sam Chr3 | samtools view filter.bam
```

5. What would be the result of the following command? 
```bash
samtools view -bh -s 0.2 aln1.bam
```
* A `BAM` file with 20% randomly-sampled reads from the original `BAM`
* A `BAM` file with the highest-scoring (`MAPQ`) 20% reads from the original `BAM`
* An invalid `BAM` file
* A `BAM` file reads covering 20% of the genome








