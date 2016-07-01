# Lesson 06: For Loops

## Loops
Loops can really improve productivity through automation as they allow us to execute commands repetitively. Like to wildcards and tab completion, using loops also reduces the amount of typing (and typing mistakes). 

In the next portion, we will build loops that do something to a large number of files. Hopefully, you will so learn some best practices so that you don't do something you will immediately regret. 

### echo $i

~~~ {.bash}
$ for i in SRR534005*
> do
>    echo $i
> done
~~~

~~~ {.output}
SRR534005_01_R1.fastq
SRR534005_01_R2.fastq
SRR534005_02_R1.fastq
SRR534005_02_R2.fastq
SRR534005_03_R1.fastq
SRR534005_03_R2.fastq
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
SRR534005_01_R1.fastq
SRR534005_01_R2.fastq
SRR534005_02_R1.fastq
SRR534005_02_R2.fastq
SRR534005_03_R1.fastq
SRR534005_03_R2.fastq
~~~

**Note:** Sometimes instead of typing `echo $whatever` you actually need to type `echo ${whatever}`. This is especially true when you are inserting it into a line with other characters. In the same way that the quotes were necessary for `echo 'hello!!'` but not for `echo 'hello'`, sometimes the {} and mandatory and sometimes the {} are optional.

### echo $file copy-$file

Let's say we want to make a copy and give that copy a new name. Before we actually do that, its good to test what the new name will look like with echo

~~~ {.bash}
$ for file in *.fastq
> do
>    echo ${file} copy-${file}
> done
~~~

~~~ {.output}
SRR534005_01_R1.fastq copy-SRR534005_01_R1.fastq
SRR534005_01_R2.fastq copy-SRR534005_01_R2.fastq
SRR534005_02_R1.fastq copy-SRR534005_02_R1.fastq
SRR534005_02_R2.fastq copy-SRR534005_02_R2.fastq
SRR534005_03_R1.fastq copy-SRR534005_03_R1.fastq
SRR534005_03_R2.fastq copy-SRR534005_03_R2.fastq
~~~

Now, we can see the current name and the potential new name. 

### cp $file copy-$file

To actually make the change, we can replace `echo` with `cp`.

If you use the up arrow on your keyboard, you will notice that the for loop can be viewed on a single line, with some subtly difference in formatting. You can move over and replace the `echo` with `cp` so that you don't have to type it all out

~~~ {.bash}
$ for file in SRR534005*; do cp $file copy-$file; done
~~~

### Rename the middle of a file

The SRR534005 name isn't very informative, and it doesn't fit well with the flow of our data. There are lots of ways to rename things, but let's explore parameter expansion.

~~~ {.bash}
$ for file in copy-SRR534005*; do echo $file ${file//SRR534005/chicken}; done
~~~

~~~ {.output}
copy-SRR534005_01_R1.fastq copy-chicken_01_R1.fastq
copy-SRR534005_01_R2.fastq copy-chicken_01_R2.fastq
copy-SRR534005_02_R1.fastq copy-chicken_02_R1.fastq
copy-SRR534005_02_R2.fastq copy-chicken_02_R2.fastq
copy-SRR534005_03_R1.fastq copy-chicken_03_R1.fastq
copy-SRR534005_03_R2.fastq copy-chicken_03_R2.fastq
~~~

What we have done here is echo the file but we have replaced the SRR thing with chicken.  Now to make the replacement we can use the `mv` command.

~~~ {.bash}
$ for file in copy-SRR534005*; echo $file ${file//SRR534005/chicken}; do mv $file ${file//SRR534005/chicken}; done
~~~

~~~ {.output}
copy-chicken_01_R1.fastq
copy-chicken_01_R2.fastq
copy-chicken_02_R1.fastq
copy-chicken_02_R2.fastq
copy-chicken_03_R1.fastq
copy-chicken_03_R2.fastq
SRR534005_01_R1.fastq
SRR534005_01_R2.fastq
SRR534005_02_R1.fastq
SRR534005_02_R2.fastq
SRR534005_03_R1.fastq
SRR534005_03_R2.fastq
~~~



## Proceed to the Previous lesson
**Next Lesson** [07 Bash Scripts](https://github.com/raynamharris/Shell_Intro_for_Transcriptomics/blob/master/lessons/07_BashScripts.md)
**Previous Lesson** [05 grep, uniq, and history](https://github.com/raynamharris/Shell_Intro_for_Transcriptomics/blob/master/lessons/05_FindingThings.md) 