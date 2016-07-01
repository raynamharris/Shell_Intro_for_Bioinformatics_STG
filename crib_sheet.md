# Crib Sheet: Intro to Unix
<br><br>


Command | Translation | Examples
--------|-------------|---------
`cd` | **c**hange **d**irectory | `cd /absolute/path/of/the/directory/` <br> Go to the home directory by typing simply  `cd` or `cd ~` <br> Go up (back) a directory by typing `cd ..`
`pwd` | **p**rint **w**orking **d**irectory | `pwd`
`mkdir` | **m**ake **dir**ectory | `mkdir newDirectory` creates newDirectory in your current directory <br> Make a directory one level up with `mkdir ../newDirectory`
`cp` | **c**o**p**y | `cp file.txt newfile.txt` (and file.txt will still exist!)
`mv` | **m**o**v**e | `mv file.txt newfile.txt` (but file.txt will *no longer* exist!)
`rm` | **r**e**m**ove | `rm file.txt` removes file.txt <br> `rm -r directoryname/` removes the directory and all files within
`ls` | **l**i**s**t | `ls *.txt` lists all .txt files in current directory <br> `ls -a` lists all files including hidden ones in the current directory <br> `ls -l` lists all files in current directory including file sizes and timestamps <br> `ls -lh` does the same but changes file size format to be **h**uman-readable <br> `ls ../` lists files in the directory above the current one <br> `ls -lrS` lists files sorted by size in reverse <br> `ls -lt` lists files sorted by time <br> `ls -lx` lists files sorted by file extension
`man` | **man**ual | `man ls` opens the manual for command `ls` (use `q` to escape page)
`grep` | **g**lobal **r**egular <br> **e**xpression **p**arser |  `grep ">" seqs.fasta` pulls out all sequence names in a fasta file <br> `grep -c ">" seqs.fasta` counts the number of those sequences <br> 
`cat` | con**cat**enate | `cat seqs.fasta` prints the contents of seqs.fasta to the screen (ie stdout)
`head` | **head** | `head seqs.fasta` prints the first 10 lines of the file <br> `head -n 3 seqs.fasta` prints first 3 lines
`tail` | **tail** | `tail seqs.fasta` prints the last 10 lines of the file <br> `tail -n 3 seqs.fasta` prints last 3 lines
`wc` | **w**ord **c**ount | `wc filename.txt` shows the number of new lines, number of words, and number of characters <br> `wc -l filename.txt` shows only the number of new lines <br> `wc -c filename.txt` shows only the number of characters
`sort` | **sort** | `sort filename.txt` sorts file and prints output
`uniq` | **uniq**ue | `uniq -u filename.txt` shows only unique elements of a list <br> (must use sort command first to cluster repeats)

Shortcut | Use
----------|-----
Ctrl + C | kills current process
Ctrl + L | clears screen
Ctrl + A | Go to the beginning of the line
Ctrl + E | Go to the end of the line
Ctrl + U | Clears the line before the cursor position
Ctrl + K | Clear the line after the cursor
`*` | wildcard character
tab | completes word
Up Arrow | call last command
`.` | current directory
`..` | one level up 
`~` | home
`>` | redirects stdout to a file, *overwriting* file if it already exists
`>>` | redirects stdout to a file, *appending* to the end of file if it already exists
`|` | redirects stdout to become stdin for next command