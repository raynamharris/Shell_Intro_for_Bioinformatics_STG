# Lesson 05: grep, uniq, and history

## grep

In the same way that many of us now use “Google” as a verb meaning “to find”, Unix programmers often use the word “grep”. “grep” is a contraction of “global/regular expression/print”, a common sequence of operations in early Unix text editors. It is also the name of a very useful command-line program.

For our examples, we will use a file that contains three haikus taken from a 1998 competition in Salon magazine. For this set of examples we’re going to be working in the manuscripts directory that is in the same level as our data directory. To get there `cd` up a level with `..` then into manuscripts.

~~~ {.bash}
$ cd ../manuscripts
~~~

The command `grep` finds and prints lines in files that match a pattern. The useage is grep <pattern> <filenmame>.

Let’s find lines that contain the word “not” in haiku.txt. The output is the three lines in the file that contain the letters “not”.

~~~ {.bash}
$ grep not haiku.txt
~~~

~~~ {.output}
Is not the true Tao, until
"My Thesis" not found
Today it is not working
~~~

Now, let's try a different example, using the pattern "day".

~~~ {.bash}
$ grep day haiku.txt
~~~

~~~ {.output}
Yesterday it worked
Today it is not working
~~~

### grep -w

This time, two lines that include the letters “day” are outputted. However, these letters are contained within larger words. To restrict matches to lines containing the word “day” on its own, we can give grep with the -w flag. This will limit matches to word boundaries.

~~~ {.bash}
$ grep -w day haiku.txt
~~~

You can put quotes around the pattern, especially if you have spaces. 

~~~ {.bash}
$ grep -w "is not" haiku.txt
~~~

~~~ {.output}
Today it is not working
~~~

### grep -n

Another useful option is -n, which numbers the lines that match:

~~~ {.bash}
$ grep -n it haiku.txt
~~~

~~~ {.output}
5:With searching comes loss
9:Yesterday it worked
10:Today it is not working
~~~

## grep -i -v 

Just like with `ls -lht`, we can combine flags. For example, let’s find the lines that contain the word “the”. We can combine the options `-w`, `-i`, and `-n` to find the lines that contain the word “the”, to be case insensitive and also find "The", and to number the lines that match.

~~~ {.bash}
$ grep -n -w -i the haiku.txt
~~~

~~~ {.output}
1:The Tao that is seen
2:Is not the true Tao, until
6:and the presence of absence:
~~~

Then, we can use the `-v` options to invert the output to print only lines the **do not** match.

~~~ {.bash}
$ grep -n -w -i -v the haiku.txt
~~~

~~~ {.output}
3:You bring fresh toner.
4:
5:With searching comes loss
7:"My Thesis" not found.
8:
9:Yesterday it worked
10:Today it is not working
11:Software is like that.
~~~

## grep -A 1

Now, if we think back to Scott's one liner, he used the `-A 1` flag to **also print one line after** the line matching. Let's look at an example.

~~~ {.bash}
$ grep -w "is not" haiku.txt
~~~

~~~ {.output}
Today it is not working
~~~

~~~ {.bash}
$ grep -w -A 1 "is not" haiku.txt
~~~

~~~ {.output}
Today it is not working
Software is like that.
~~~

## uniq 

The `uniq` command  recognizes when two or more *adjacent lines* are the same. The flag `-c` counts how many identical lines there were and prepends the count to the line itself. The flag `-w N` only uses the first N characters of each line to decide if they're the same. Because of the *adjacent* requirement, you typically `sort` before executing the `uniq` command. 

~~~ {.bash}
$ sort haiku.txt | uniq -c 
~~~

~~~ {.output}
   2 
   1 "My Thesis" not found.
   1 Is not the true Tao, until
   1 Software is like that.
   1 The Tao that is seen
   1 Today it is not working
   1 With searching comes loss
   1 Yesterday it worked
   1 You bring fresh toner.
   1 and the presence of absence:
~~~

## history

The `history` command will print a recent history of the commands you have typed. 

~~~ {.bash}
$ history 
~~~

Like everything else, you can pipe the results of your history to a new file or through another string of commands

~~~ {.bash}
$ history | grep "pwd"
~~~

~~~ {.output}   
  77   pwd
  232  pwd
  236  pwd
  243  pwd
  557  history | grep "pwd" 
~~~


# Challenge: Search your history to see what commands you use most frequently

1. How many times did you change directories today?
2. How many times did you use the pipe today?
3. How many times did you look at the contents of a directory today?

# 
Moral of the story: Most of what we do at the command line is navigate directories with `cd` and `ls`. 


## Proceed to the Next or Previous lesson
**Next Lesson:** [06 For Loops](https://github.com/raynamharris/Shell_Intro_for_Transcriptomics/blob/master/lessons/06_ForLoops.md)    
**Previous Lesson** [04 Pipes and Filters](https://github.com/raynamharris/Shell_Intro_for_Transcriptomics/blob/master/lessons/04_PipesFilters.md)