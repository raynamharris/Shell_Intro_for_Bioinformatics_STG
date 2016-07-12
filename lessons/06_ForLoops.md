# Lesson 06: For Loops

## Learning Objectives
- Know what a variable is 
- Know the general structure of a unix for loop
- Use a for loop to echo through a list of files
- Use a for loop to create a list of commands to run the fastqc program on a list of files
- Use a for loop to create a list of commands to run the trimmomatic program on a list of files

## Motivating Dataset

For this exercise, lets got into our "myfirstsbatch" directory and list the contents. 

~~~ {.bash}
$ cd ~/work/myfirstsbatch/wc_reads_better
$ ls
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
 
You will notice that we have 8 files representing paired end reads for 4 samples.

## Loops
Loops can really improve productivity through automation as they allow us to execute commands repetitively. Like to wildcards and tab completion, using loops also reduces the amount of typing (and typing mistakes). 

In the next portion, we will build loops that do something to a large number of files. Hopefully, you will so learn some best practices so that you don't do something you will immediately regret. 

### echo $i

~~~ {.bash}
$ for i in *.fastq
> do
>    ls $i
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

### ls $file and echo $file

Sometimes, it helps to use something a little more descriptive that "i" or "j". So you can describe this. For instance, these are all files.


~~~ {.bash}
$ for file in *.fastq
> do
>    ls $file
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

`echo` is an alternative to ls for printing to the screen.

~~~ {.bash}
$ for file in *.fastq
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

The awesome thing about `echo` is that you can print the file name AND a bunch of other stuff to the screen. But, you have to put that stuff inside double quotes

~~~ {.bash}
$ for file in *.fastq
> do
>    echo "Do something to $file" today.
> done
~~~ 

Now, are you starting to see how we can use this to build a list of commands? Let's try this with a simple-ish program.

## For loop with fastq

~~~ {.bash}
$ for file in *.fastq
> do
>    echo " fastq $file"
> done
~~~

~~~ {.output}
fastqc GM_25_S_S31_L003_R1_001_small.fastq
fastqc GM_25_S_S31_L003_R2_001_small.fastq
fastqc GM_26_S_S32_L003_R1_001_small.fastq
fastqc GM_26_S_S32_L003_R2_001_small.fastq
fastqc PD_10_S_S27_L003_R1_001_small.fastq
fastqc PD_10_S_S27_L003_R2_001_small.fastq
fastqc PD_11_S_S28_L003_R1_001_small.fastq
fastqc PD_11_S_S28_L003_R2_001_small.fastq
~~~

**Note:** If you want to echo a command, you need to put the command inside double quotes so that it will look inside the quotes and replace the variable with the file. When using single quotes, the variable will not be replaced.

**Note:** Sometimes instead of typing `echo $whatever` you actually need to type `echo ${whatever}`. This is especially true when you are inserting it into a line with other characters. In the same way that the quotes were necessary for `echo 'hello!!'` but not for `echo 'hello'`, sometimes the {} and mandatory and sometimes the {} are optional.


## Using for loops on R1 and R2 separately

We can do this selectively for a subset of our files, like for instance the R1 reads. Let's create a variable name that reflects that these are R1 files.

First, what would you type to list all the R1 reads?
~~~ {.bash}
$ ls *R1*
~~~

~~~ {.bash}
$ for R1 in *R1*
> do
>    echo $R1
> done
~~~

~~~ {.output}
GM_25_S_S31_L003_R1_001_small.fastq
GM_26_S_S32_L003_R1_001_small.fastq
PD_10_S_S27_L003_R1_001_small.fastq
PD_11_S_S28_L003_R1_001_small.fastq
~~~

Using the R1 variable, we can create and R2 variable using some magic. There are multiple ways to do this. One way is to use some replace commands like this: `newvariablename=${oldvariablename//oldtext/newtext}`. Here is an example

~~~ {.bash}
$ for R1 in *R1*
> do
>    R2=${R1//R1_001_small.fastq/R2_001_small.fastq}
>    echo $R1 $R2
> done
~~~

Now, if we want to do something to both files, we can add some text inside double quotes.  

~~~ {.bash}
$ for R1 in *R1*
> do
>    R2=${R1//R1_001_small.fastq/R2_001_small.fastq}
>    echo "do something to $R1 and also to $R2
> done
~~~

~~~ {.bash}
do something to GM_25_S_S31_L003_R1_001_small.fastq and to GM_25_S_S31_L003_R2_001_small.fastq as well
do something to GM_26_S_S32_L003_R1_001_small.fastq and to GM_26_S_S32_L003_R2_001_small.fastq as well
do something to PD_10_S_S27_L003_R1_001_small.fastq and to PD_10_S_S27_L003_R2_001_small.fastq as well
do something to PD_11_S_S28_L003_R1_001_small.fastq and to PD_11_S_S28_L003_R2_001_small.fastq as well
~~~

## Using for loops to run Trimmomatic

Here is the general structure for the Trimmomatic command for paried end reads.

`java -jar <path to trimmomatic.jar> PE -threads 32 -phred33 <R1.fastq> <R2.fastqc> <R1-paired.fastq.gz>  <R1-unpaired.fastq.gz> <R2-paired.fastq.gz> <R2-unpaired.fastq.gz>`

With this, we can see that we need 6 variable names. You might want to construct this inside a text file! Because we're doing this in a text file, I'll write this without the bash prompts.

~~~ {.bash}
for R1 in *R1*
do
   R2=${R1//R1_001_small.fastq/R2_001_small.fastq}
   R1paired=${R1//.fastq/_paired.fastq.gz}
   R1unpaired=${R1//.fastq/_unpaired.fastq.gz}	
   R2paired=${R2//.fastq/_paired.fastq.gz}
   R2unpaired=${R2//.fastq/_unpaired.fastq.gz}	
   echo $R1 $R2 $R1paired $R1unpaired $R2paired $R2unpaired
done
~~~

Now, our results looks something like this.

~~~ 
GM_25_S_S31_L003_R1_001_small.fastq GM_25_S_S31_L003_R2_001_small.fastq GM_25_S_S31_L003_R1_001_small_paired.fastq.gz GM_25_S_S31_L003_R1_001_small_unpaired.fastq.gz GM_25_S_S31_L003_R2_001_small_paired.fastq.gz GM_25_S_S31_L003_R2_001_small_unpaired.fastq.gz
GM_26_S_S32_L003_R1_001_small.fastq GM_26_S_S32_L003_R2_001_small.fastq GM_26_S_S32_L003_R1_001_small_paired.fastq.gz GM_26_S_S32_L003_R1_001_small_unpaired.fastq.gz GM_26_S_S32_L003_R2_001_small_paired.fastq.gz GM_26_S_S32_L003_R2_001_small_unpaired.fastq.gz
PD_10_S_S27_L003_R1_001_small.fastq PD_10_S_S27_L003_R2_001_small.fastq PD_10_S_S27_L003_R1_001_small_paired.fastq.gz PD_10_S_S27_L003_R1_001_small_unpaired.fastq.gz PD_10_S_S27_L003_R2_001_small_paired.fastq.gz PD_10_S_S27_L003_R2_001_small_unpaired.fastq.gz
PD_11_S_S28_L003_R1_001_small.fastq PD_11_S_S28_L003_R2_001_small.fastq PD_11_S_S28_L003_R1_001_small_paired.fastq.gz PD_11_S_S28_L003_R1_001_small_unpaired.fastq.gz PD_11_S_S28_L003_R2_001_small_paired.fastq.gz PD_11_S_S28_L003_R2_001_small_unpaired.fastq.gz
~~~

Finally, let's modify this script to write a Trimmomatic command. The timmomatic command requres that you give the path to the program. This program is over in our work direcotry.  You should be able to use the variable `$WORK` to get to your work folder.



~~~ {.bash}
for R1 in *R1*
do
   R2=${R1//R1_001_small.fastq/R2_001_small.fastq}
   R1paired=${R1//.fastq/_paired.fastq.gz}
   R1unpaired=${R1//.fastq/_unpaired.fastq.gz}	
   R2paired=${R2//.fastq/_paired.fastq.gz}
   R2unpaired=${R2//.fastq/_unpaired.fastq.gz}	
   echo "java -jar $WORK/IntMolModule/STG/practiceData/Trimmomatic-0.36 PE -threads 32 -phred33 $R1 $R2 $R1paired $R1unpaired $R2paired $R2unpaired"
done
~~~

~~~ {.bash}
java -jar /work/02189/rmharris/IntMolModule/STG/practiceData/Trimmomatic-0.36 PE -threads 32 -phred33 GM_25_S_S31_L003_R1_001_small.fastq GM_25_S_S31_L003_R2_001_small.fastq GM_25_S_S31_L003_R1_001_small_paired.fastq.gz GM_25_S_S31_L003_R1_001_small_unpaired.fastq.gz GM_25_S_S31_L003_R2_001_small_paired.fastq.gz GM_25_S_S31_L003_R2_001_small_unpaired.fastq.gz
java -jar /work/02189/rmharris/IntMolModule/STG/practiceData/Trimmomatic-0.36 PE -threads 32 -phred33 GM_26_S_S32_L003_R1_001_small.fastq GM_26_S_S32_L003_R2_001_small.fastq GM_26_S_S32_L003_R1_001_small_paired.fastq.gz GM_26_S_S32_L003_R1_001_small_unpaired.fastq.gz GM_26_S_S32_L003_R2_001_small_paired.fastq.gz GM_26_S_S32_L003_R2_001_small_unpaired.fastq.gz
java -jar /work/02189/rmharris/IntMolModule/STG/practiceData/Trimmomatic-0.36 PE -threads 32 -phred33 PD_10_S_S27_L003_R1_001_small.fastq PD_10_S_S27_L003_R2_001_small.fastq PD_10_S_S27_L003_R1_001_small_paired.fastq.gz PD_10_S_S27_L003_R1_001_small_unpaired.fastq.gz PD_10_S_S27_L003_R2_001_small_paired.fastq.gz PD_10_S_S27_L003_R2_001_small_unpaired.fastq.gz
java -jar /work/02189/rmharris/IntMolModule/STG/practiceData/Trimmomatic-0.36 PE -threads 32 -phred33 PD_11_S_S28_L003_R1_001_small.fastq PD_11_S_S28_L003_R2_001_small.fastq PD_11_S_S28_L003_R1_001_small_paired.fastq.gz PD_11_S_S28_L003_R1_001_small_unpaired.fastq.gz PD_11_S_S28_L003_R2_001_small_paired.fastq.gz PD_11_S_S28_L003_R2_001_small_unpaired.fastq.gz
~~~

## Writing to command files

Now, we can copy and past this into a commands file. You can save this as a text file, but you can also save it with the `.cmds` extension which is a common way to identify files that contain a list of commands. 

~~~ {.bash}
rm trimmomaticcommands.cmds
for R1 in *R1*
do
   R2=${R1//R1_001_small.fastq/R2_001_small.fastq}
   R1paired=${R1//.fastq/_paired.fastq.gz}
   R1unpaired=${R1//.fastq/_unpaired.fastq.gz}	
   R2paired=${R2//.fastq/_paired.fastq.gz}
   R2unpaired=${R2//.fastq/_unpaired.fastq.gz}	
   echo "java -jar $WORK/IntMolModule/STG/practiceData/Trimmomatic-0.36 PE -threads 32 -phred33 $R1 $R2 $R1paired $R1unpaired $R2paired $R2unpaired" >> trimmomaticcommands.cmds
done
cat trimmomaticcommands.cmds
~~~ 

It is good practie to add a line to remove any .cmds file that might be there already so we dont' apppend.

Now, who can we exectue this file?


## Proceed to the Previous lesson
**Next Lesson** [07 Bash Scripts](https://github.com/raynamharris/Shell_Intro_for_Transcriptomics/blob/master/lessons/07_BashScripts.md)
**Previous Lesson** [05 grep, uniq, and history](https://github.com/raynamharris/Shell_Intro_for_Transcriptomics/blob/master/lessons/05_FindingThings.md) 