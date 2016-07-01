# Lesson 06: For Loops

## Loops
Loops can really improve productivity through automation as they allow us to execute commands repetitively. Like to wildcards and tab completion, using loops also reduces the amount of typing (and typing mistakes). 

In the next portion, we will build loops that do something to a large number of files. Hopefully, you will so learn some best practices so that you don't do something you will immediately regret. 

### echo $i

~~~ {.bash}
$ for i in *.fastq
> do
>    echo $i
> done
~~~

~~~ {.output}
GM_25_S_S31_L003_R1_001_small.fastq
GM_25_S_S31_L003_R2_001_small.fastq
GM_26_S_S32_L003_R1_001_small.fastq
GM_26_S_S32_L003_R2_001_small.fastq
PD_10_S_S27_L003_R1_001_small.fastq
PD_10_S_S27_L003_R2_001_small.fastq
PD_11_S_S28_L003_R1_001_small.fastq
PD_11_S_S28_L003_R2_001_small.fastq
~~~

Let's break this down. 
- When the shell sees the keyword `for`, it knows it is supposed to repeat a command (or group of commands) once for each thing in a list. 
- In this case, the list will contain all the files in the directory ending with `.fastq` because we said match the pattern `*.fastq`.
- Each time through the loop, the name of the thing in the list currently being operated on is assigned to the variable called `i`. 
- Inside the loop, we get the variable’s value by putting $ in front of it: `$i` is `SRR534005_01_R1.fastq` the first time through the loop and `SRR534005_03_R2.fastq` the last time. 
- `do` tells the shell that we are about to give it some commands
- the command that’s actually being run is our old friend echo will print the value of `i` on the screen
- `done` lets the shell know the process is complete

### echo $file

Sometimes, it helps to use something a little more descriptive that "i" or "j". So you can describe this. For instance, these are all files.


~~~ {.bash}
$ for file in SRR534005*
> do
>    echo $file
> done
~~~

~~~ {.output}
GM_25_S_S31_L003_R1_001_small.fastq
GM_25_S_S31_L003_R2_001_small.fastq
GM_26_S_S32_L003_R1_001_small.fastq
GM_26_S_S32_L003_R2_001_small.fastq
PD_10_S_S27_L003_R1_001_small.fastq
PD_10_S_S27_L003_R2_001_small.fastq
PD_11_S_S28_L003_R1_001_small.fastq
PD_11_S_S28_L003_R2_001_small.fastq
~~~

**Note:** Sometimes instead of typing `echo $whatever` you actually need to type `echo ${whatever}`. This is especially true when you are inserting it into a line with other characters. In the same way that the quotes were necessary for `echo 'hello!!'` but not for `echo 'hello'`, sometimes the {} and mandatory and sometimes the {} are optional.

### wc of all files

If we want to count the number of reads in all our files and see the name of the file, we need to use a for loop.

~~~ {.bash}
$ for file in *.fastq
> do
>    echo $file
>    cat $file | grep '^@K00179' | wc -l 
> done
~~~

~~~ {.output}
GM_25_S_S31_L003_R1_001_small.fastq
     100
GM_25_S_S31_L003_R2_001_small.fastq
     100
GM_26_S_S32_L003_R1_001_small.fastq
      25
GM_26_S_S32_L003_R2_001_small.fastq
      25
PD_10_S_S27_L003_R1_001_small.fastq
      50
PD_10_S_S27_L003_R2_001_small.fastq
      50
PD_11_S_S28_L003_R1_001_small.fastq
      75
PD_11_S_S28_L003_R2_001_small.fastq
      75
~~~

Now, we can the name of the file and the number of reads for each file!

If we want to save the output in our results folder, rather than print to the screen, we redirect and append the output. 

~~~ {.bash}
$ for file in *.fastq
> do
>    echo $file 
>    cat $file | grep '^@K00179' | wc -l >> ../results/numberrawreads.txt
> done
~~~

## Proceed to the Previous lesson
**Next Lesson** [07 Bash Scripts](https://github.com/raynamharris/Shell_Intro_for_Transcriptomics/blob/master/lessons/07_BashScripts.md)
**Previous Lesson** [05 grep, uniq, and history](https://github.com/raynamharris/Shell_Intro_for_Transcriptomics/blob/master/lessons/05_FindingThings.md) 