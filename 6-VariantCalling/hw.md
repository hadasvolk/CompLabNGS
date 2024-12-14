# Lesson 6 exercise

In this exercise we will detect variants between the wine yeast *RM11* and the reference genome of the *S288C* strain. We’ll call short variants using `bcftools` and then visualize and filter the results. Finally, we’ll try to detect structural variants based on short read data, using `Manta-SV`.

## Part I - short variant calling

Download the file `S288C_reference_sequence_R64-2-1_20150113.fasta` from the [data](https://github.com/hadasvolk/CompLabNGS/tree/main/6-VariantCalling/data) directory.

First, index the reference genome using the `samtools faidx` command. What does this it mean to index a fasta file?

Use `bcftools mpileup`, followed by `bcftools call` to create variant calls. Use the high-quality mappings sorted `BAM` from you generated in previous HW assignment as input (either your own results or the ones found in *data/SRR1569760_vs_S288C.HQ.sort.bam*). 

To save on run time, we’ll only call variants on one of the yeast chromosome. Use `-r ChrII` in `bcftools mpileup` to limit the search to second chromosome of the yeast genome.

While you’re waiting for the calling process to complete, let’s prepare an `IGV` session for visualizing the results. Open `IGV`. Make sure the *S288C* reference genome is loaded (download and load it if needed) and then load the high-quality `BAM` file you are using for variant calling (`File → Load from file`). Once the file is loaded, select *ChrII* and zoom in on some region until you see the read mappings.

Try identifying positions where you think variants between the *RM11* sequence and the reference might exist, based on read mapping. Mark the selected regions by clicking the `define region of interest` button  and then clicking the borders of the regions. This is a useful feature that allows you to easily come back to these regions later.

#### Q1: Find positions of three such cases and explain why you think they contain a variant, and what type of variant.

When you’re done exploring, save the `IGV` session by choosing `File → Save session` and save it to your directory.

Go back to your terminal and look at the `VCF` file with variant calls.

#### Q2: How many variants were detected?

Load the `VCF` file into your `IGV` session (`File → Load from file`). Click `Regions → Region Navigator` and zoom to each of the saved regions.

#### Q3: Were the variants detected as you expected?

Filter the variants vcf to create a high-quality variants set only containing calls with variant `quality >= 30` and `read depth >= 10` (use `bcftools view -i`).

#### Q4: How many variants are left? What is the average variant frequency (Number of variants/chromosome size)? (hint: use `IGV` to find the size of chromosome 2). Are the variants distributed more or less equally along the chromosome?

## Part II - structural variant calling
 
Create the `Manta-SV` configuration by running: 
```bash
configManta.py --bam <HQ sorted bam> --referenceFasta S288C_reference_sequence_R64-2-1_20150113.fasta --runDir Manta
```
* Replace <HQ sorted bam> with your filtered `BAM` file.
  
Follow the instructions printed to the screen to run the analysis.

The main output can be found in `Manta/results/variants/diploidSV.vcf.gz`

View the file `diploidSV.vcf` using `less`. The [`Manta-SV` user guide](https://github.com/Illumina/manta/blob/master/docs/userGuide/README.md#manta-vcf-interpretation) explains the specifics of the software’s output.

#### Q5: How many SVs were found in total? How many on chromosome 2? How many Deletions? (hint: use the `SVTYPE ID`).

Load `diploidSV.vcf` to `IGV`.

#### Q6: Look at a region containing a structural variant, report the position as Chromosome:start-end. What type of `SV` is this? Do the read mapping support this `SV`? Explain why you think so.

## Part III - variant calling with `GATK`

`GATK` is a popular tool for variant calling. It is a bit more complicated to use than `bcftools`, but it is also more powerful. We will use `GATK` to call variants on the same `BAM` file we used for `bcftools` variant calling. We'll need to prepare the `BAM` file for `GATK` by adding read group information to it.

Start by adding read group information to your bam file. You can do this by running something like:
```bash
gatk AddOrReplaceReadGroups -I <your .bam file> -O <.bam file with read group> -LB READS -PL ILLUMINA -PU 1 -SM SRR1569760 --CREATE_INDEX
```

`GATK` will only take `FASTA` files with a `.fasta` extension, so if your reference `FASTA` is called anything else, change the name (as well as the fasta index file name).

`GATK` also requires a dictionary file alongside the fasta reference. What is the purpose of this file?

Create a `dict` file for the `FASTA` using 
```bash
gatk CreateSequenceDictionary -R reference.fasta -O reference.dict
```

Now use the `BAM` file you created to run `GATK`’s `HaplotypeCaller`:
```bash
gatk HaplotypeCaller -R <ref fasta> -I  <bam with read groups> -O <output vcf> -L ChrII
```
* Replace `<ref fasta>` with the reference fasta file, and `<bam with read groups>` with the bam file you created with read groups.

Use the same filtration criteria as you did above to filter the output vcf and get a high-quality set of variants.

#### Q7: How many variants were detected before and after filtration?

Load the high-quality `VCF` to `IGV`.

#### Q8: Are the results similar to the results of `bcftools`? Can you tell which software is correct in this case?
