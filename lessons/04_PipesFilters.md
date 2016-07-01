# Lesson 04: Pipes and Filters

Rather than creating complex programs that do many different things, Unix programmers focus on creating simple tools that each do one job well. The simple tools can then be combined with one another to carry out more complex processes. This programming model is called “pipes and filters”. The key is that any program that reads lines of text from standard input and writes lines of text to standard output can be combined with every other program that behaves this way as well. 

To illustrate this concept, lets learn a few new commands and tricks and then learn how to string them together.

## wc

The **word count** command  `wc <filename>` counts the number of lines, words, and characters in the specified file.

To count the number of lines, words, and characters in our fastq.gz files, let's run the  command `wc SRR534005_01_R1.fastq`.

~~~ {.bash}
$ wc SRR534005_01_R1.fastq
~~~
~~~ {.output}
     400     500   26200 SRR534005_01_R1.fastq
~~~

This tells us there there are 400 lines, 500 words, and 26200 characters in this file

## * 
A `*` is known as a wildcard, and it matches zero or more characters. In this directory, `human*` would match `human_01_R1.fastq.gz` and `human_02_R1.fastq.gz`. Another example is that `*R2.fastq.gz` would match all the read 2s (aka R2) that are zipped.

A `?` is also a wildcard, but it only matches a single character. This could be useful for capturing both read 1 and read 2 for a particular sample. For example,  `SRR534005_01_R?.fastq.gz` would match `SRR534005_01_R1.fastq.gz` and `SRR534005_01_R2.fastq.gz`

When the shell sees a wildcard, it expands the wildcard to create a list of matching filenames *before* running the command that was asked for. 

Let's try this with a new command.

## gunzip

Since fastq.gz files are in binary, we can't read them. Let's unzip these files using the command `gunzip` followed by the file name. We can either give a single file, or we can use wildcards to unzip multiple files at once.

~~~ {.bash}
$ gunzip SRR534005_01_R2.fastq.gz
$ ls
$ gunzip *.gz
$ ls
~~~

## wc (continued)

Now that we've unzipped our files. Let's revisit wc

~~~ {.bash}
$ wc *.fastq
~~~

### wc -l 

We can add the flag `-l` to return just the number of lines

~~~ {.bash}
$ wc -l *.fastq
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

# BONUS: Scott's list of UNIX one liner's

Are you beginning to see how this is useful?  You can string together many commands to answer specific questions. 

For instance, to answer "Are there any unusually abundance sequences in my human_rnaseq.fastq file?", we could execute this one liner

~~~ {.bash}
$ head -100000 yeast_01_R1.fastq | grep -A 1 '^@HWI' | grep -v '^@HWI' | sort | uniq -c | sort -n -r | head
~~~

I strongly recommend bookmarking [Scott's List of Unix One Liners](https://wikis.utexas.edu/display/bioiteam/Scott's+list+of+linux+one-liners) for future reference.

In the meantime, lets take a look at grep in more detail.


## Proceed to the Next and Previous lessons
**Next Lesson:** [05 grep, uniq, and history](https://github.com/raynamharris/Shell_Intro_for_Transcriptomics/blob/master/lessons/05_FindingThings.md)     
**Previous Lesson:** [03 Read Write Move Copy](https://github.com/raynamharris/Shell_Intro_for_Transcriptomics/blob/master/lessons/03_ReadWriteMoveCopy.md)