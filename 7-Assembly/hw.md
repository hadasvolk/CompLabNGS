# Lesson 7 exercise

In this exercise you will explore various factors affecting assembly quality. You’ll do that using the *RM11* yeast strain genome. Since genome assembly is a computationally-intense and time consuming process even for small genomes, you won’t have to perform the assemblies yourself. 

Instead,  you will use the assemblies prepared for you in advance, which differ from each other by the input data.

The following table contains the details regarding the assemblies you will analyze:

| Data set ID | Sequencing depth | Library layout* |
|:-----------:|:----------------:|:---------------:|
| 1 | 5 | 2x101 PE, IS 200 |
| 2 | 10 | 2x101 PE, IS 200 |
| 3 | 30 | 2x101 PE, IS 200 |
| 4 | 100 | 2x101 PE, IS 200 |
| 5 | 200 | 2x101 PE, IS 200 |
| 6 | 30 | 2x101 PE, IS 2000 |
| 7 | 30 | 1x101 SE |
| 8 | 15 | 2x101 PE, IS 200 |
| 9 | 15 | 2x101 PE, IS 2000 |
* PE = paired-end; SE = single-end; IS = insert size (bp)

All assemblies are available as Fasta files under [data/all_assemblies](https://github.com/hadasvolk/CompLabNGS/tree/main/7-Assembly/data/all_assemblies)

Note that for each assembly you have both a *contigs* and a *scaffolds* file.

QA will be performed using `QUAST`. You can use the manual if you need.

We’ll start by focusing on **assembly 4**. This will help you get the idea, after which we can start comparing between assemblies.

Run `QUAST` simultaneously on assembly 4 contigs and scaffolds. This can be done using the command:
```bash
quast <path to contigs fasta> <path to scaffolds fasta> -o <output directory> -m 1 -t 1
```
(we use `-m 1` to consider contigs of all sizes, and `-t 1` to limit `QUAST` to using one CPU core)

When `QUAST` is done, open the `report.html` file using a web browser (the same way we viewed `FastQC` reports). Take a moment to make sure you understand the report and to click the various buttons to see what they do.

#### Q1: complete the following table with the relevant assembly stats:

| Stat | Contigs | Scaffolds |
|:----:|:-------:|:---------:|
| Assembly size | | |
| N50 | | |
| N90* | | |
| % gaps | | |
* Use the interactive **Nx** plot and try to get as close as possible to **N90**

Repeat the `QUAST` analysis, but this time provide additional data to assess assembly accuracy. Two `bam` files are available under `data`, with input reads mapped to the assembly contigs and scaffolds. Provide them to `QUAST` (in addition to the parameters used above) using `--bam <contigs.bam>,<scaffolds.bam>` (note: separate with comma without space). 

Also provide the *S288C* reference genome using the `-r` option followed by the path to the reference fasta [6-VariantCalling/data/S288C_reference_sequence_R64-2-1_20150113.fsa](https://github.com/hadasvolk/CompLabNGS/blob/main/6-VariantCalling/data/S288C_reference_sequence_R64-2-1_20150113.fsa).

When `QUAST` is done, open the new report. Click the “Extended report” button and notice the new sections added to the report.

#### Q2: How many misassemblies were detected in the scaffolds? What percentage of the assembly is affected by misassemblies?

#### Q3: What is the percentage of the contigs assembly not covered by any read?

Finally, we’ll use `BUSCO` to assess the completeness of the assembled scaffolds. Since the `BUSCO` run takes a while, we’ll use pre-computed results. You can find the results under: [data/BUSCO_assembly4](https://github.com/hadasvolk/CompLabNGS/tree/main/7-Assembly/data/BUSCO_assembly4)

#### Q4: Look at the short_summary_BUSCO.txt file - how many BUSCOs are in the test set? What is the percentage of complete BUSCOs detected in the scaffolds?

Next, we’ll explore the effect of sequencing depth on assembly contiguity and completeness. To keep things simple, we’ll focus on contigs **N50** and assembly size only. Run `QUAST` on the contigs of assemblies 1-5 and look at the report. You can also use a software like `Excel` to plot the stats as a function of sequencing depth.

#### Q5: Which of the stats (contiguity or completeness) is more affected by the sequencing depth? AAre the stats linearly dependent on the depth, or are they saturated? What do you think will be the result if we increase the depth to 400x?

Finally, we will analyze the effect of the library layout. To this end, we will compare scaffolds from assemblies 3,6,7, and 8, all with a total depth of 30x. Run `QUAST` on these assemblies and analyze the report.

#### Q6: Summarize the results in a few sentences. Describe your observations regarding the effect of using paired-end vs. single-end reads and the effect of the library insert size. Which layout produces the best assembly?