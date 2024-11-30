# Lesson 4 exercise

In this exercise we’ll continue analyzing the *RM11* wine yeast data set. We’ll compare the gene sequences of the *RM11* strain to the laboratory strain *S288C* genome using `BLAST`. We’ll need the yeast reference genome of the *S288C* strain and the gene set of *RM11* from the **data** directory.

#### Q1: How many records are in each FASTA file? What do the records represent in each file?

Create a `BLAST` DB for the *S288C* genome. You can use `help` to find out which parameters are needed 
```bash
makeblastdb -help
``` 

Let’s start by *blasting* one *RM11* gene against the *S288C* genome. 

Create a file that contains only the first fasta record (gene *EDV08516*) of **RM11_genes.fasta** (use any command/method you see fit).

Use `BLAST` (which command is suitable?) to search for the gene within the *S288C* genome DB.

Look at the blast output.

#### Q2: was the gene found? How many hits? If there is more than one, which is the best? What’s the genomic location? Do you think this is a reliable hit (look at the alignment and consider the various scores)?

Now that we are comfortable with the `BLAST` output, let’s take a more global look by *blasting* all *RM11* genes against the *S288C* genome. You may want to set some **E-value** threshold to avoid low quality hits (use the option `-evalue`). You can also try different output formats using the `-outfmt` option (tabular format 6 is especially useful) and the `-max_target_seqs` option.

Look at the result. If you used the tabular output format, take a look at this page for explanations of the columns. Look for the gene you *blasted* to verify that results make sense.

#### Q4: How many of the *RM11* genes were found in the *S288C* genome? Remember that each gene may appear multiple times (why?), so you’ll need to use a combination of some Linux commands to get the right answer.

##### Hint: try some combination of the `cut`, `sort` and `uniq` commands.

Create a list of the *RM11* genes not found in the *S288C* genome.
##### Hint: no need to rerun `BLAST` - this can be extracted from the `BLAST` output using Linux command line.

#### Q4: How many of the mapped genes had a perfect match (i.e. no mismatches and no gaps)?
