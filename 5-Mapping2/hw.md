# Lesson 5 exercise

In this exercise we’ll use `BWA` for short read alignment and then analyze the results. We will map reads of the *RM11* strain to the *S288C* genome. The results will be used in the next lesson for variant calling.

We’ll use the cleaned reads data created in **Lesson3**. You can either use the data you created or take the relevant data from the [Lesson3 data directory](https://github.com/hadasvolk/CompLabNGS/tree/main/3-QC/data).


Download the *S288C* [reference genome fasta](https://github.com/hadasvolk/CompLabNGS/tree/main/4-Mapping1/data/S288C_reference_sequence_R64-2-1_20150113.fsa) from the **data** directory of the previous lesson.

Create a `BWA` index for the reference.

Use `bwa mem` to map the *RM11* reads to the *S288C* reference. This may take a few minutes to complete.

Once your run is done, take a while to inspect the resulting `SAM` file. Make sure you understand the various fields. Choose a few `SAM` flags and interpret them using the `SAM` decoder.

#### Q1: What fraction of your input reads was “mapped in proper pair”?

#### Q2: What fraction of your input reads was “mapped in proper pair” with `MAPQ >= 30`? You can try a few other MAPQ cutoffs and choose one you think is reasonable.

Create a `BAM` file containing only reads which pass the above filtration criteria. Remember to include the header lines in the `BAM` file.

Sort your `BAM` file, then create a `BAM` index. This will allow more efficient processing in downstream analyses.

Use the command `samtools stats` on the resulting `BAM` file. This will calculate various statistics. Redirect (>) the output to a file so you can explore it easily. If you want, you can adjust your filtration criteria and rerun.

#### Q3: How many pairs are mapped on different chromosomes? Now, create a `BAM` file for all the reads (without the `MAPQ >= 30` and “mapped in proper pair” criteria). How many pairs are mapped on different chromosomes in this case?

Download and install the `IGV` browser from [here](http://software.broadinstitute.org/software/igv/download). You can download `IGV` for your operating system, or if you use **WSL2**, you can download the Linux version with anaconda.
```bash
conda install igv
```

Open `IGV`. Make sure the *S288C* genome is selected (if not, select it from the genomes dropdown. If it’s not there, load it: `Genomes → Load genome from file`, then choose the fasta file).

Load the high-quality sorted, indexed `BAM` file you created (`File → Load from file`) and explore your alignment results:
* Zoom in until you see the coverage (depth) and alignment tracks.

#### Q2: Hover with your mouse over the coverage track and give an estimate of the average depth of the data.

* Try different views by right-clicking the alignments track and changing between “Collapsed”, “Squished” and “Expanded“, then try “View as pairs”.

#### Q5: Why are some reads colored in blue and red? You can hover over such reads to view their information and/or use the `IGV` documentation.

#### BONUS Q6: Can you locate reads with suspected sequencing errors? How about real SNPs? Describe how to distinguish between them.
