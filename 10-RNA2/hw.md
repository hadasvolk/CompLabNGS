# Lesson 10 exercise

In this exercise we continue our differential gene expression analysis, comparing transcription profiles between the *S288C* (reference) and *RM11* strains. 

### Experiment design: 
*S288C* and *RM11* were grown in optimal conditions, then total *mRNA* was extracted, and libraries were prepared (using a stranded protocol) and sequenced. This experiment was replicated three times, so a total of six samples were sequenced.

* Note: the `BAM` files are available in the Google Drive folder, as they are too large to be stored in the GitHub repository. [Gdrive](https://drive.google.com/drive/folders/1N1pYkeFPUOo4_Hv_Jk2MzgzlZ-LLWXSY?usp=sharing)

### Data processing: 
RNA-seq reads were cleaned and mapped to the *S288C* reference genome using `STAR`, the same way you did in lesson 8. Resulting `BAM` files were filtered, sorted, and indexed. These `BAM` files are the starting point for our analysis today.

Our main tool in the analysis would be the `DeSeq2` Python package, `PyDESeq`. We will use it to perform the differential gene expression analysis and visualize the results.

## Preparing count matrix

We will start by creating a count matrix from the `BAM` files. This matrix will be used as input for the differential gene expression analysis. We will use the `featureCounts` tool from the `subread` package to count the number of reads that map to each transcript.

```bash
featureCounts -p -a Saccharomyces_cerevisiae.R64-1-1.60.gtf -o counts.tsv -t exon -g transcript_id *.bam
```

#### Q1: Why did we use the `-p` flag in the `featureCounts` command?

#### Q2: What is the meaning of the `-t exon` and `-g transcript_id` flags?

Review the output of the `featureCounts` command. The resulting file, `counts.tsv`, contains the count matrix. Each row in the file represents a transcript, and each column represents a sample. The values in the matrix are the number of reads that map to each transcript in each sample.

#### Q3: How many transcripts are in the count matrix?

## Differential gene expression analysis

We will use the `PyDESeq2` package to perform the differential gene expression analysis.

* Note: The `PyDESeq2` package needs to be installed using `pip`, it is not aviailable in the `conda` package manager.

```bash
pip install pyDESeq2
```

You will need to read the `counts.tsv` file into a `pandas` dataframe in order to use `PyDESeq2`. Keep in mind that the `PyDESeq2` package expects the count matrix to be in the form of a `pandas` dataframe, with the rows representing the samples and the columns representing the transcripts. featureCounts included a header in the output file, so you will need to skip the first row when reading the file into a dataframe, and to drop irrelevant columns.

Filter the data such that only transcripts with at least 10 reads in at least one sample are kept. This will speed up the analysis and reduce noise levels.

#### Q4: How many transcripts are left after filtering?

### Sample similarity QA
Before we proceed to the actual DE analysis, we can create a simple test to see which samples are most similar and make sure this matches our knowledge about the experiment design.

Create the sample-to-sample similarity matrix using the `pandas` dataframe. This matrix will be used to visualize the similarity between samples.

```python
import seaborn as sns

sns.clustermap(counts.corr())
```

#### Q5: What do you observe in the sample-to-sample similarity matrix? Do samples from the same strain cluster together? How about samples from the same batch?

A file containing the sample information about each of the six is also needed. Namely, from which strain each sample came and in which experiment batch. A simple TSV file was prepared for you, `sample_info.tsv`. Load this file as a `pandas` dataframe as well with sample names as index.

* Note: make sure the counts dataframe columns names match the sample_info dataframe index.

Next, you will need to create a `DESeqDataSet` object from the count matrix and the sample information. This object will be used to perform the differential gene expression analysis.

```python
from pydeseq2.dds import DeseqDataSet
from pydeseq2.default_inference import DefaultInference
from pydeseq2.ds import DeseqStats

inference = DefaultInference(n_cpus=8)
dds = DeseqDataSet(
    counts=counts.T,
    metadata=sample_info,
    design_factors=['condition'],
    refit_cooks=True,
    inference=inference
)

dds.deseq2()

ds = DeseqStats(dds, contrast=['condition', 'YMR253C', 'WT'])
print(ds.summary())
```

#### Q6: What is the meaning of each of the columns in the results table?

#### Q7: How many genes have Log2FoldChange > 1 and adjusted p-value < 0.05?

#### Q8: Create a volcano plot to visualize the results of the differential gene expression analysis.

To detect differentially expressed genes, we will use 0.01 as padj cutoffs and 1 as  log2FoldChange cutoff. Remember: log2FoldChange = 1 means that expression level was twice as high.

#### Q9: How many DE genes were detected?
#### Q10: What would be the result of increasing padj_cutoff? How about lfc_cutoff? Explain. (If you are not sure, you can try out different cutoffs)





