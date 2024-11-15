# Test Yourself

1. Which of the following can lead to phasing issues in an Illumina run?
   
* Chain terminator not cleaved
* Incomplete wash of fluorescent bases
* Insufficient availability of fluorescent bases
* Incorporation of a wrong base
* Wrong fluorescent signal interpretation

2. In a Fastq file, what is the probability that a base call with Q indicator `<` is correct?
* 0.998
* 0.002
* 0.95
* 0.07
* 0.5

3. Which of the following can cause biased per-base sequence content, as indicated in the FastQC plot?
* Over-representation of specific sequences in the data
* Non-random fragmentation of genomic DNA during library preparation
* A bias towards very large insert sizes created during library preparation
* A genome with extreme genomic GC content (e.g. 20% GC 80% AT)

4. What will the following `trimmomatic` command do? You may want to look at the `trimmomatic` manual.
```bash
trimmomatic PE -basein my_reads_R1.fastq -baseout my_reads AVGQUAL:28 TRAILING:20 MINLEN:70
``` 
* Discard reads shorter than 70 bp
* Discard reads with average Q score < 28
* Trim bases from read end if they have Q score < 20
* Trim 20 bases from the end of the read
* Trim bases found in windows with average Q score < 28
* Trim all reads to length 70 by removing bases from the end

5. In which of the following library designs would read merging be a reasonable step?
* PE, insert size 250, read length 150
* SE, insert size 250, read length 150
* PE, insert size 350, read length 100
* PE, insert size 400, read length 150
