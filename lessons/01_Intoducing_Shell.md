# Lesson 01. Introducing the Shell

## Background
The **shell** is a command line interface program that allows you to control your computer with a keyboard rather than using your mouse and keyboard to control your computer through a graphical user interface (GUI). It may seem strange and difficult at first, but there are  many reasons master the shell.

* Most bioinformatics programs can only be run from the command line. So, you will have to become familiar with the shell if you want to work in genomics or transcriptomics.
* The shell gives the you power to do your work more efficiently and more quickly. This is the first step toward developing a reproducible research program.
* Cloud computers can only be accessed through command line interfaces.

## How to Access the Shell
The shell is already available on Mac and Linux machines. Windows users will have to download a separate program.

### Mac
On a Mac, the Unix Shell is available through the program **Terminal**. To open the Terminal, go to:   

Applications -> Utilities -> Terminal    
Or
Type Terminal in the Spotlight Search   

You may want to drag the Terminal application to your Dock for easy access.

### Windows
On Windows machines, you will need to download a program. There are many to choose from, bit [Git Bash](http://msysgit.github.io) is very novice-friendly. Git Bash is already installed on the Machines in FAC.

## Getting Starting with the Git Bash on Windows

When you open the program Git Bash, you should see something that looks like the following:

~~~ {.output}
rmharris@CNS-FAC101BP16 ~
$
~~~

The first line indicated the user and the computer `user@computer` as well as the path. In this case, the path is indicated by `~`, which is a shorthand for the root directory. We will discuss this in the next lesson.
The `$` is a **prompt**, which shows us that the shell is waiting for you to type. 

**Note:** When following along and typing commands from these lessons, do not type the $; only type the commands that follow it.

## Configuring Text Editors

### Using Notepad++Configuring Git Bash to work with Notepad++

Notepadd++ is great for writing scripts because the formatting helps you understand your code. Git Bash doesn't have a text editor, but we can make ours work with notepad (but not notepad++. To configure it for notepad, type the following"

~~~ {.bash}
$ git config --global core.editor "'c:/program files (x86)/Notepad++/notepad++.exe' - multiInst -notabbar -nosession -noPlugin"
$ alias notepad="'c:/program files (x86)/Notepad++/notepad++.exe'"
~~~

Then, to open a bash script from the command line type:

~~~ {.bash}
$ notepad <name_of_file>.sh
~~~

### Using Text Wrangler

Text Wrangler is great for writing scripts because the formatting because the formatting helps you understand your code. 

To make TextWrangler the default:

1. "Get Info" on a text file in the Finder.
2. Change the "Open with:" program to TextWrangler, in the fifth information pane.
3. Click the "Change All..." button at the bottom of the pane.


## Proceed to the Next or Previous lesson
**Next Lesson:** [02 Navigating Directories](https://github.com/raynamharris/Shell_Intro_for_Transcriptomics/blob/master/lessons/02_Navigating_Dirs.md)  
**Previous Lesson** [00 The Motivating Dataset](https://github.com/raynamharris/Shell_Intro_for_Transcriptomics/blob/master/lessons/00_Motivating_Dataset.md)