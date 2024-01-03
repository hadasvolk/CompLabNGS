# Lesson 2 exercise

This exercise has two sections. We’ll start with some Linux drills to practice basic command line work. We’ll then learn to use the Blast command line interface (CLI) as an example for working with bioinformatic software.

## Part 1 - Linux basics

Let’s get some data to work with. We want to copy the file *2-Linux/data/UP000000625_83333.fasta* to your local machine/server you are working on. We can download it from GitHub or use a ```wget``` command to fetch via the terminal
```bash
wget https://raw.githubusercontent.com/hadasvolk/CompLabNGS/main/2-Linux/data/UP000000625_83333.fasta
```
This text file contains all protein sequences of the E. coli bacteria, in fasta format. If you’re not familiar with this format, make a quick Google search to get the idea.

#### Q1: What is the size of the file? (use the command ```ls -lh``` to get a human-readable size)

Take a moment to decide what command would work best to view the file, then use it and take a look at the data to understand the format.

Let’s give the file a more suitable name - rename it to *e_coli_proteins.fasta*

#### Q2: How many lines are in the file? How many proteins are in the E. coli proteome?

#### Q3: Fetch all protein headers labeled with **DNA polymerase** and write them into a new file called *e_coli_dna_pol*. How many are there?

## Part 2 - Blast

Blast is one of the most widely used bioinformatic tools. We’ll discuss it in detail in lesson 4, but for now we’ll just make an initial introduction and practice usage of command line software. “Blast” stands for “basic local alignment search tool”, and is useful for searching a database of sequences (nucleotides or amino acids) for matches with specific sequences (e.g. genes). If you have never worked with Blast, you may want to take a look at the [wiki](https://en.wikipedia.org/wiki/BLAST_(biotechnology))

While Blast has a good web interface, command line usage gives us more control and better performance. Therefore, we’ll learn to use it in this exercise section.

Let's install the software using either ```conda``` or ```apt``` (in case you are using Ubuntu based Linux distribution). If you are using ```conda``` you can install it by running:
```bash
conda install -c bioconda blast
```
If you are using ```apt``` you can install it by running:
```bash
sudo apt install ncbi-blast+
```

We’ll start by creating a blast database (DB) from the E. coli proteins fasta. This step is necessary for us to be able to search the protein sequences. The command that performs this task is ```makeblastdb```.

Start by viewing the usage instructions with ```makeblastdb -help``` or ```makeblastdb -help | less```. In our simple case, we only need the basic options ```-in```, ```-dbtype``` and ```-input_type```. Determine the parameter values (reminder: -help) and run the command. 

Redirect output and error messages to the files *makeblastdb.out* and *makeblastdb.err* by using the ```>``` and ```2>``` syntax.

Are there any error messages in *makeblastdb.err*? If there are, it means your run failed. Try fixing the problems and rerun until you get an empty file.

#### Q1: Look at *makeblastdb.out*. It contains information about the run such as the start date, duration and number of proteins processed (in technical terms, this is usually called the run “log”). How many sequences were added to the Blast DB?

#### Q2: What new files were created by the command? (hint: try ```ls -ltr```)

Now that we have a DB, let’s run a few test searches to see that everything works as expected. The file *2-Linux/data/test_proteins.fasta* contains 5 protein sequences taken from the E. coli proteins set, so they should obviously be found when searched against our DB. Another random sequence was added as negative control. To blast sequences against a DB, we used the commands ```blastn``` (for nucleotides) and ```blastp``` (for proteins). Use ```blastp -help``` to get an idea of the inputs and outputs.

Blast the test set against the DB by running:
```bash
blastp -query <query fasta> -db <DB> -outfmt 7 -out test_proteins.blast
```
complete the relevant parameters:
```-query <query fasta>``` - the fasta file that contains the proteins we want to search

```-db <DB>``` - the fasta file we used in order to build the DB

```-outfmt 7``` - output the results as a table

```-out test_proteins.blast``` - print results to file rather than to screen

When the run is complete, look at the output file. Notice the lines starting with **#**, which indicate table headers. Make sure that each of the test proteins found a perfect match, and that the random sequence didn’t.

#### Q3: How many hits does the protein *sp|A0A385XJL2|YGDT_ECOLI* have? How many are perfect matches (100% identity)?

Now that we’ve tested Blast a bit, let’s use it to find putative gene orthologs from the bacteria species *Shigella dysenteriae*. The file *2-Linux/data/s_dysenteriae_proteins.fasta* contains the S. dysenteriae proteome. We will Blast the proteins against the E. coli DB. To ensure we only get high quality matches, add the parameter ```-evalue 0.0001```. We also want to display only the best hit for each query, so we use ```-max_target_seqs```. Run the analysis (this may take a minute or two) and look at the resulting blast output. 

To extract interesting proteome-scale information we’ll need some more advanced tools that we’ll learn later in the course, so for now just make sure you understand the output by looking at one example: PQN05807.

#### Q4: Search the blast output for PQN05807 (hint: use ```grep```). What is the name of the E. coli protein to which PQN05807 matched? What is the % of sequence identity?
