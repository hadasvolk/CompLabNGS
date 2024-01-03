# Test Yourself
1. Which of the following commands will list all and only files in the current directory that end with “.bam” and also contain the word “genome”?

```bash
ls *genome*.bam
```

```bash
ls -l *.bam | grep genome
```

```bash
ls *.bam | grep genome
```

```bash
grep *genome*.bam
```

```bash
grep ‘.bam’ | grep genome
```

```bash
ls -l *genome* *.bam
```

2. Assuming your current dir is /path/to/cool/dir , which of the following commands will create a new directory /path/to/bar?

```bash
cd ../../ ; mkdir bar
```

```bash
mkdir ../../bar
```

```bash
mkdir /path/to/bar
```

```bash
touch /path/to/bar
```

```bash
cd ./ ; cd ./ ; mkdir bar
```

```bash
touch ~/to/bar
```

```bash
cd ; mkdir path/to/bar
```

3. The file *numbers.txt* contains 200 lines, each containing a number. How many distinct (unique) numbers are in the file? You will need the Linux command ```uniq```, but note that it only works on sorted files. Hint: the command you need contains pipes.

4. What is the size of the file you get when taking only the first 24 lines of the file  *2-Linux\data\UP000000625_83333.fasta* (as given by ```ls -lh```)?

5. Use the command ```grep --help | less ``` to view full usage instructions for the grep command. Which flag will print the line number/s in which the pattern was found?
