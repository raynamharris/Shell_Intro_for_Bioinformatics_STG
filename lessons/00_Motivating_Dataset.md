# Lesson 00. The Motivating Dataset

## Background
The focus of this workshop is on working with data and data management for genomics research. The workshop does not teach any particular bioinformatics tools, but the foundational skills that will allow you to conduct any analysis and analyze the output of a genomics pipeline.

## Download the FASTQ Files for today

1. Visit this website: https://github.com/raynamharris/DataForUnixCourse
2. Click **Downlad Zip**
3. Navigate to your Downloads folder
4. Extract all the files
5. Move the folder **"DataForUnixCourse"** to your desktop

## FASTQ Files
FASTQ format is a text-based format for storing both a biological sequence and a corresponding quality scores. The quality scores are encoded with a single ASCII character for brevity.

A FASTQ file normally uses four lines per sequence.

**Line 1** begins with a '@' character and is followed by a series of information that uniquely identifies each read. Thus, this is our sequence. Here are two example:

@HWI-ST1097:127:C0W5VACXX:5:1101:4820:2124 1:N:0:CTCAGA  
@SRR534005.299 HWI-ST945:93:c02g4acxx:3:1101:16012:2225/1  

**Line 2** is the raw sequence. The lenght of this sequence should correspond to the length of the read requested (i.e. 75 bp, 150 bp). These are AGTC or N uppercase characters.

**Line 3** is always '+' for output from the Illumina machines in the Genomic Sequencing and Analysis Facility. 

**Line 4** is a string of Ascii-encoded base quality scores encodes the quality values for the sequence in Line 2. This string contain the same number of symbols as letters in the sequence on Line 2.

## Proceed to the Next Lesson
**Next Lesson:** [01 Introducing the Shell](https://github.com/raynamharris/Shell_Intro_for_Transcriptomics/blob/master/lessons/01_Intoducing_Shell.md) 