# Lesson 3 exercise

In this exercise we’ll introduce a data set that we’ll keep revisiting throughout the course.
The data set is taken from a whole genome sequencing project of a yeast strain called *RM11*, which is used in wine production.
Today we’ll QC the raw data and preprocess them for downstream analysis.

### Download relevent tools

You can download all needed software for today's exercise using conda.

Below is an example command to create a conda environment called `lesson3` and install all needed software in it.

```bash
conda create -n lesson3 -c bioconda fastqc trimmomatic fastuniq flash
```
In order to activate the environment, run:
```bash
conda activate lesson3
```
You should see `(lesson3)` at the beginning of your command line prompt.

## __

Start by simply looking at each file and making sure the data format is OK. Make sure read titles make sense and match between R1 and R2.

Keep in mind that the data is paired-end, and that the two files contain the forward and reverse reads, respectively. Also, the data is in fastq gzipped format. You can use `zcat` to look at the files without unzipping them.

#### Q1: what is the difference between the header of the first read in R1 and the header of the first read in R2?

#### Q2:  What is the read length? (hint - use echo and wc) How many reads are there per file? Use these counts to estimate sequencing depth, assuming a genome size of 12Mb.

To get some general QC stats on the data, run `FastQC` on the two fastq files (R1 and R2).
You can run FastQC on both files in parallel by running:
```bash
fastqc -o fastqc_results -t 2 *.fastq.gz
```
The output will be written to the `fastqc_results` directory as html files. You can view these files in any web browser.

#### Q3: Look at the resulting html files. Notice anything strange? Write the name of the suspicious plot. Also, is there any differences between R1 and R2? 

Use `trimmomatic` to clean up your data. You can use the `FastQC` results to help you decide on which cleanup modules to apply, and with what parameters.

Note: you can use the **NexteraPE-PE.fa** file to remove sequencing adapters.

#### Q4: Report the command and the parameters you used and explain why you chose them.

After `trimmomatic` is finished, look at the stats printed to the screen and re-analyze the output _1P and _2P files (by rerunning `FastQC`). Decide if cleanup results are satisfying, and if needed, adjust the parameters and rerun `trimmomatic`.

#### Q5: What is the depth of the sequencing after cleanup?


### Bonus section (optional)
Use `fastuniq` to remove PCR (or other) duplicates from the clean paired reads. You’ll need to create a file with the list of fastq files you want to de-duplicate. 

To do that:

Type ```vi fastuniq_files```

Press the **i** key. You are now in edit mode. 

Paste/type the relevant file names, one per line, e.g:

*SRR1569760_1P*

*SRR1569760_2P*

When you are done editing, press **Esc** and then **:x** and **Enter** to save and exit.

Run ```cat fastuniq_files``` to make sure the file looks OK. Make sure the file doesn’t contain empty lines.

Now you can run `fastuniq` (start by running without arguments to get the help message)

You may also try to merge read pairs using `FLASH`, although this result won’t be necessary for now.
