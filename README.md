# LeTRS
LeTRS was implemented in Perl programming language, including a main program for identification of leader-TRS junctions and a script for plotting graphs of the results. It accepts fastq files derived from illumina paired-end and nanopore cDNA/direct RNA sequencing, and bam files produced by a splicing alignment method with a sars-cov-2 genome. By default, LeTRS analyses the sars-cov-2 by using 11 known leader-TRS junctions and an NCBI reference genome (NC_045512.2), but user can also provide customize leader-TRS junctions and sars-cov-2 or other coronavirus genome as reference.

1. Installation:
(1) Three party tools dependences:
samtools (>=1.11)
hisat2(>=2.1.0)
minimap2(>=2.17)
portcullis(=1.1.2)

We suggest to install the portcullis with conda as below:
conda install portcullis=1.1.2 --channel=bioconda

(2) Perl module dependences:
Getopt::Long
File::Basename
List::Compare
List::Util
List::Uniq
use Statistics::R

(3) R module dependences (for plotting):
ggplot2

2. Usages 
Please see the details of each parameters by:

Examples:
(1) To analyse ARTIC V3 noropore cDNA sequencing data and extract the reads contain the identified leader-TRS junctions in fasta format:

perl LeTRS.pl -t 16 -extractfasta -Rtch cDNA -mode noropore -fa example.fastq.gz -primer_bed primer_V3.bed -o LeTRS_output 

(2) To analyse direct RNA noropore sequencing data and extract the reads contain the identified leader-TRS junctions in fasta format:

perl LeTRS.pl -t 16 -extractfasta -Rtch RNA -mode noropore -fq example.fastq.gz -o LeTRS_output

(3) To analyse direct RNA noropore sequencing data with customize leader-TRS junctions and sars-cov-2 or other coronavirus genome as reference, and extract the reads contain the identified leader-TRS junctions in fasta format:perl LeTRS.pl -t 16 -extractfasta -Rtch RNA -mode noropore -fq example.fastq.gz -o LeTRS_output -ref reference_folder

(4) To analyse paired end illumina sequencing data and extract the reads contain the identified leader-TRS junctions in fasta format:

perl LeTRS.pl -t 16 -extractfasta -mode illumia -fq #1.fasq.gz:#2.fasq.gz -primer_bed primer_V3.bed -o LeTRS_output

(5) To analyse customize bam file reads derived from any platform aligned by using a splicing mapping method.

perl LeTRS.pl -t 16 -extractfasta -mode illumia -bam example.bam -o LeTRS_output

3. Plotting  
There is also a perl script that can plot a diagram for the output of LeTRS.pl.

Examples:
(1) Plotting the value in the column of peak_count in "known_junction.tab" or nb_count in the "novel_junction.tab. -count 1 indicates the first number of each row in the column and -count 2 indicates the second number of each row in the column, and so on.

perl LeTRS-plot.pl -count 1 -i known_junction.tab
 
(2) Plotting the value in the column of peak_peak_count_ratio in "known_junction.tab" or count_ratio in the "novel_junction.tab. -count 1 indicates the first number of each row in the column and -count 2 indicates the second number of each row in the column, and so on.

perl LeTRS-plot.pl -ratio 1 -i known_junction.tab


4. Customize leader-TRS junctions and sars-cov-2 or other coronavirus genome as reference.
Please the see the readme.txt file in the making_reference_folder_example folder.

