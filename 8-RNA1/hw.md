# Lesson 8 exercise

In this exercise you will perform the first part of a differential gene expression analysis. We want to compare expression profiles between the *S288C* and *RM-11* yeast strains under optimal growth conditions.

We’ll start from RNA-seq reads, process them, then map the reads to a reference genome and QA the results. We’ll get to the read counting and determination of differentially expressed genes steps in the next lesson.

The data contains experimental replicates, each with ~30M reads. However, due to the long run times of some of the steps, you’ll only work with a subsample from a single experiment. The full data will be prepared for your use in the next lesson.

The `S288C_RNA-seq_rep1_subsample.fq.gz` is a small subsample from one of six RNA-seq experiments (three replicates per strain). Note that single-end (SE) sequencing was used.

Start by running `FastQC` on the file to get a general idea of the data quality (go back to lesson 3 if you don’t remember how).

Use `Trimmomatic` to filter low-quality reads. Remember that we have 50bp SE reads and configure `Trimmomatic` accordingly. 

Rerun `FastQC` to make sure filtration went fine. 

#### Q1: What percentage of the data was filtered?

Next, we’ll map the filtered RNA-seq reads to the reference genome using `STAR`. 

First, we need to create an index. 

Create a directory called *S288C_reference_sequence_R64-2-1_20150113.STAR*, then run `STAR` to create the indexed genome in this directory.

The reference genome (`fasta`) and annotation (`gtf`) are available in the `data` dir. You’ll need to include the option `--genomeSAindexNbases 10` to avoid warning/error messages.

Before we perform the actual mapping, we need to determine the maximal intron size we want to use. While most yeast genes don’t have introns, some do, as can be seen in the `gff` file. We can use the **intron** features in the annotation file along with some Linux tricks to determine the largest intron size. Just run:
```bash
awk '$3 == "intron" {print $5 - $4}' S288C_reference_annotation_proc.gff | sort -nr | less
```

#### Q2: What is the maximal intron length in the yeast genome?

Run `STAR` again, this time to map the clean reads to the reference genome. Use the `--alignIntronMax <X>` option, with <X>  being the largest intron size + 20%. 

Also use `--outSAMtype BAM SortedByCoordinate`, to tell `STAR` to produce a sorted `BAM` output. The run should take a few minutes, so use `&` to send your command to background.

While you’re waiting for the run to complete, open an `IGV` session and load the reference genome and annotation.

When `STAR` is finished, you should see the output file `Aligned.sortedByCoord.out.bam`

Index the `BAM` file.

Load the `BAM` file to `IGV` and take some time for exploration. Particularly, pay attention to factors like the depth distribution and uniformity between genes and intergenic regions.

Here are four examples of yeast genes containing introns:
```bash
YDL083c    YEL003W    YKL180W    YNL162W
```

You can simply paste a gene name into the search box in `IGV` and hit Enter to zoom to a specific gene.

#### Q3: Are there reads mapped to the intronic regions? Were the splice junctions detected correctly? Write two example locations

Finally, we’ll run `Qualimap` for a more systematic QA of the mapping. Use the sorted `BAM` file as input. Since `Qualimap` can only take `gtf` (and not `gff`) files as genome annotations, you should use the file `S288C_reference_annotation_proc.gtf`.

You’ll find the report under a new directory called `<input bam>_rnaseq_qc`. Open the file `qualimapReport.html` with a web browser.

Make sure you understand the meaning of the different statistics. Use [this document](http://qualimap.conesalab.org/#id7) for details.

#### Q4: Based on the *Strand specificity estimation* result, is this a strand-specific RNA-seq library? If yes, is it in forward or reverse orientation?

Rerun `Qualimap` using the `-p` option with a value matching the library prep protocol. You can run `qualimap rnaseq -h` to find the possible values for the `-p` option.

#### Q5: What is the percentage of reads mapped to the genome? What is the percentage of reads mapped to the genes?