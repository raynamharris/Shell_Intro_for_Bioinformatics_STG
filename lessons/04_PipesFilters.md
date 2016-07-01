# Lesson 04: Pipes and Filters

Rather than creating complex programs that do many different things, Unix programmers focus on creating simple tools that each do one job well. The simple tools can then be combined with one another to carry out more complex processes. This programming model is called “pipes and filters”. The key is that any program that reads lines of text from standard input and writes lines of text to standard output can be combined with every other program that behaves this way as well. 

To illustrate this concept, lets learn a few new commands and tricks and then learn how to string them together.

## wc

The **word count** command  `wc <filename>` counts the number of lines, words, and characters in the specified file.

To count the number of lines, words, and characters in our fastq.gz files, let's run the  command `wc SRR534005_01_R1.fastq`.

~~~ {.bash}
$ wc GM_25_S_S31_L003_R1_001_small.fastq
~~~
We see that there are 400 files in the file. Since there are 4 lines per read, we know that we have 100 reads in this sample.

~~~ {.output}
     400     500   35873 GM_25_S_S31_L003_R1_001_small.fastq
~~~

This tells us there there are 400 lines, 500 words, and 26200 characters in this file

## * 
A `*` is known as a wildcard, and it matches zero or more characters. In this directory, `GM*` would match all the reads from GM cells. Another example is that `*R2.fastq` would match all the 2nd pairs of the paired-end reads (aka R2).

A `?` is also a wildcard, but it only matches a single character. This could be useful for capturing both read 1 and read 2 for a particular sample. For example,  `GM_2?_S_S31_L003_R1_001_small.fastq` would match `GM_25_S_S31_L003_R1_001_small.fastq` and `GM_26_S_S32_L003_R1_001_small.fastq`

When the shell sees a wildcard, it expands the wildcard to create a list of matching filenames *before* running the command that was asked for. 

Let's try this with a new command.

## wc (continued)

Let's revisit `wc` and count all the lines in our files

~~~ {.bash}
$ wc *.fastq
~~~

~~~ {.output}
     400     500   35873 GM_25_S_S31_L003_R1_001_small.fastq
     400     500   35873 GM_25_S_S31_L003_R2_001_small.fastq
     100     125    8968 GM_26_S_S32_L003_R1_001_small.fastq
     100     125    8968 GM_26_S_S32_L003_R2_001_small.fastq
     200     250   17941 PD_10_S_S27_L003_R1_001_small.fastq
     200     250   17941 PD_10_S_S27_L003_R2_001_small.fastq
     300     375   26912 PD_11_S_S28_L003_R1_001_small.fastq
     300     375   26912 PD_11_S_S28_L003_R2_001_small.fastq
    2000    2500  179388 total
~~~

### wc -l 

We can add the flag `-l` to return just the number of lines

~~~ {.bash}
$ wc -l *.fastq
~~~

~~~ {.output}
     400 GM_25_S_S31_L003_R1_001_small.fastq
     400 GM_25_S_S31_L003_R2_001_small.fastq
     100 GM_26_S_S32_L003_R1_001_small.fastq
     100 GM_26_S_S32_L003_R2_001_small.fastq
     200 PD_10_S_S27_L003_R1_001_small.fastq
     200 PD_10_S_S27_L003_R2_001_small.fastq
     300 PD_11_S_S28_L003_R1_001_small.fastq
     300 PD_11_S_S28_L003_R2_001_small.fastq
    2000 total
~~~

### wc -w 

We can add the flag `-w` to return just the number of words

~~~ {.bash}
$ wc -w *.fastq
~~~

### wc -c 

We can add the flag `-c` to return just the number of characters

~~~ {.bash}
$ wc -c *.fastq
~~~

## > for redirection

As previously mentioned, we can redirct the output from our screen to a new file using the `>`, Then we can use `head` or `cat` to quickly view the results

~~~ {.bash}
$ wc -l *.fastq > lengths.txt
~~~

## sort

Now let's use the `sort` command with the `-n` flag to sort the lengths numerically instead of alphabetical. **Note:** only the output is sorted; the file remains in alphabetical order.

~~~ {.bash}
$ sort -n lengths.txt
~~~

We can put the sorted list of lines in another temporary file called `sorted-lengths.txt`
using the `>` redirect command. 

~~~ {.bash}
$ sort -n lengths.txt > sorted-lengths.txt
$ head -n sorted-lengths.txt
~~~

## Piping these filters together

`wc` and `sort` are filters that transforms a stream of input into a stream of output. In the previous examples, we executed two lines of code (`sort` with `>` then `head`) to print our sorted lengths to the screen. But, wouldn't it be awesome if we could do this in one step and without making a temporary file? **Yes!**

The vertical bar `|` is called a **pipe**. The pipe tells the shell that we want to use
the output of the command on the left as the input to the command on the right, without the need for making a temporary file.

~~~ {.bash}
$ sort -n lengths.txt | head
~~~

We can put lots of pipes together!

~~~ {.bash}
$ wc *.fastq | sort -n | head
~~~

**Remember** earlier we said we could use `head -100` to print the first 100 lines to the screen. Let's add `head -1` to print the smallest sequence file.

~~~ {.bash}
$ wc *.fastq | sort -n | head -1
~~~


## Proceed to the Next and Previous lessons
**Next Lesson:** [05 grep, uniq, and history](https://github.com/raynamharris/Shell_Intro_for_Transcriptomics/blob/master/lessons/05_FindingThings.md)     
**Previous Lesson:** [03 Read Write Move Copy](https://github.com/raynamharris/Shell_Intro_for_Transcriptomics/blob/master/lessons/03_ReadWriteMoveCopy.md)