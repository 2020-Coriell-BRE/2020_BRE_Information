## RNA-seq Demo Commands

This document with the RNA-seq demo processing code is set up as an example of how I structure my project documentation markdown files.

### Set Up 
*2020-07-23*

1. Create a new folder
2. Open a plain text file in a new to take notes in / document your work
3. Make that folder into a Git repository and back it up to GitHub

### Quality Control

#### Check Quality with FastQC
*2020-07-23*

```bash
# go to the rnaseq data
[kkeith]$ cd rnaseq_practice/data/
# make a folder to put the output in
[kkeith]$ mkdir fastqc
# run FastQC with a loop
[kkeith]$ fastqc *.fastq.gz -o fastqc/
```

#### Trim Adapters and Low Quality Sequences
*2020-07-23*

```bash
# still in the data directory
[kkeith]$ pwd
/home/kkeith/rnaseq_practice/data
# make a folder in the analysis folder to put the trimmed reads in
[kkeith]$ mkdir ../analysis/01_trim
# trim with trim_galore
[kkeith]$ for i in *R1.fastq.gz; do trim_galore --paired --fastqc --illumina --output ../analysis/01_trim/ --retain_unpaired -q 30 $i ${i/R1/R2}; done
```

### Process Reads

#### Align
*2020-07-23*

```bash
# go to the directory where the trimmed reads are
[kkeith]$ pwd
/home/kkeith/rnaseq_practice/data
[kkeith]$ cd ../analysis/01_trim
# make a new directory to put the aligned files in
[kkeith]$ mkdir ../02_align
# align with STAR
[kkeith]$ for i in *val_1.fq.gz; do STAR --genomeDir /mnt/data/gdata/human/hg38/chr21/STAR_index/ --readFilesIn $i ${i/R1_val_1/R2_val_2} --readFilesCommand zcat --outFileNamePrefix ../02_align/${i/R1*/} --outSAMtype BAM SortedByCoordinate; done
```

#### Count Features
*2020-07-23*

```bash
# go to the directory where the aligned reads are
[kkeith]$ pwd
/home/kkeith/rnaseq_practice/analysis/01_trim
[kkeith]$ cd ../02_align/
# make a directory to put the count tables in
[kkeith]$ mkdir ../03_count
# count the number of reads for each gene
[kkeith]$ for i in *.bam; do featureCounts -a /mnt/data/gdata/human/hg38/chr21/homo_sapiens_hg38_chr21.gtf -o ../03_count/${i/Aligned.sortedByCoord.out.bam/counts.txt} -R BAM $i; done
```
