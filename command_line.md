## Basics

### Running a terminal

1. ⌘␣
2. terminal

**iTerm** is a more advanced and customizable terminal program.

![](/Users/huangxiaosheng/Documents/learn enough/images/anatomy.png)

### Our first command

```
$ echo hello
hello
$ echo "goodbye"
goodbye
$ echo 'goodbye'
goodbye
```

When you get into trouble at the command line, your best bet is to hit **Ctrl-C**.

Note: When Ctrl-C fails, 90% of the time hitting **ESC** will do the trick.

### Man pages

```
$ man echo
ECHO(1)          BSD General Commands Manual         ECHO(1)

NAME
   echo -- write arguments to the standard output

SYNOPSIS
   echo [-n] [string ...]

DESCRIPTION
   The echo utility writes any specified operands, separated by single blank
   (` ') characters and followed by a newline (`\n') character, to the stan-
   dard output.

   The following option is available:

   -n  Do not print the trailing newline character. This may also be
      achieved by appending `\c' to the end of the string, as is done by
      iBCS2 compatible systems. Note that this option as well as the
      effect of `\c' are implementation-defined in IEEE Std 1003.1-2001
      (``POSIX.1'') as amended by Cor. 1-2002. Applications aiming for
      maximum portability are strongly encouraged to use printf(1) to
      suppress the newline character.
:                                                                             
```

You can access subsequent information one line at a time by pressing the down arrow key, or one page at a time by pressing the spacebar. To exit the man page, press “q” (for “quit”).

I recommend running `man <command name>` when encountering a new command.

### Editing the line

↑ simply retrieves the previous command. Pressing up arrow again moves further up the list of commands, while ↓ goes back toward the bottom.

type ` ⌃A` to get to the beginning of the line. `⌃E` moves to the end of the line. `⌃U` clears to the beginning of the line.

move directly to the desired spot via Option-click.

### Cleaning up

**⌃L**

## Manipulating files

### Redirecting and appending

```
$ echo "From fairest creatures we desire increase," > sonnet_1.txt
$ cat sonnet_1.txt
From fairest creatures we desire increase,
```

The name `cat` is short for “concatenate”.

```
$ echo "That thereby beauty's Rose might never die," >> sonnet_1.txt
$ cat sonnet_1.txt
From fairest creatures we desire increase,
That thereby beauty's Rose might never die,
```

```
$ echo "From fairest creatures we desire increase," > sonnet_1_lower_case.txt
$ echo "That thereby beauty's rose might never die," >> sonnet_1_lower_case.txt
```

```
$ diff sonnet_1.txt sonnet_1_lower_case.txt
< That thereby beauty's Rose might never die,
---
> That thereby beauty's rose might never die,
```

### Listing

The `ls` command can be used to check if a file (or directory) exists

```
$ ls foo
ls: foo: No such file or directory
$ touch foo
$ ls foo
foo
```

if you want to create a file, and the name doesn’t matter, the name is usually “foo”. Once you’ve used “foo”, the next file is called “bar”, the one after that “baz”.

```
$ ls *.txt
sonnet_1.txt
sonnet_1_reversed.txt
```

list the long form of all text file with a human-readable byte count:

```
$ ls -hl *.txt
total 16
-rw-r--r-- 1 mhartl staff  87 Jul 20 18:05 sonnet_1.txt
-rw-r--r-- 1 mhartl staff 294 Jul 21 12:09 sonnet_1_reversed.txt
```

```
$ ls -rtl
<results system-dependent>
```

This is particularly useful when there are a lot of files in the directory but you really only care about seeing the ones that have been modified recently, such when confirming a file download.

`-S` sorts files by size.

#### Hidden files

Hidden files and directories are identified by starting with a dot `.`, and are commonly used for things like storing user preferences.

```
$ echo "*.txt" > .gitignore
$ ls
sonnet_1.txt
sonnet_1_reversed.txt
$ ls -a
.           .gitignore      sonnet_1_reversed.txt
..          sonnet_1.txt
```

### Renaming, copying, deleting

```
$ echo "test text" > test
$ mv test test_file.txt
```

```
$ cp test_file.txt second_test.txt
```

```
$ rm second_test.txt
```

making use of *tab completion*.

```
$ rm -f *.txt
```

#### Unix terseness

the most commonly used Unix commands tend to be only two or three letters long.

## Inspecting files

### Downloading a file

Although it’s not part of the core Unix command set, the `curl` command is widely available on Unix systems. To make sure it’s available on your system, we can use the `which` command:

```
$ which curl
/usr/bin/curl
```

```
$ curl -OL https://cdn.learnenough.com/sonnets.txt
$ ls -rtl
$ mkdir images
$ curl -o images/breaching_whale.jpg \
>      -OL https://cdn.learnenough.com/breaching_whale.jpg
```

The whale picture requires attribution under the [Creative Commons Attribution-NoDerivs 2.0 Generic](https://creativecommons.org/licenses/by-nd/2.0/) license. link the image to the original attribution page.

```html
<a href="https://www.flickr.com/photos/28883788@N04/10097824543">
	<img src="images/breaching_whale.jpg">
</a>
```

Use the command `curl -I https://www.learnenough.com/` to fetch the *HTTP header*.

**Repeating previous commands**

`⌃R` lets you search through your previous commands, and then optionally edit the result before executing.

### Making heads and tails of it

The `head` command shows the first 10 lines of the file.

Similarly, `tail` shows the last 10 lines of the file.

`tail -f` views a file that’s actively changing. To simulate the creation of a log file, run `ping learnenough.com > learnenough.log` in one terminal tab. In a second tab, type the command to tail the log file.

#### Wordcount and pipes

```
$ wc sonnets.txt
  2620  17670  95635 sonnets.txt
```

Here the three numbers indicate how many lines, words, and bytes there are in the file.

```
$ head sonnets.txt | wc
   10   46   294
```

```
$ head -18 sonnets.txt | tail -n 14
From fairest creatures we desire increase,
That thereby beauty's Rose might never die,
But as the riper should by time decease,
His tender heir might bear his memory:
But thou contracted to thine own bright eyes,
Feed'st thy light's flame with self-substantial fuel,
Making a famine where abundance lies,
Thy self thy foe, to thy sweet self too cruel:
Thou that art now the world's fresh ornament,
And only herald to the gaudy spring,
Within thine own bud buriest thy content,
And tender churl mak'st waste in niggarding:
  Pity the world, or else this glutton be,
  To eat the world's due, by the grave and thee.
```

### Less is more

pressing `⌃F` to move forward a page (i.e., the same as spacebar) or `⌃B` to move back a page. `G` to move to the end of the file and `1G` (line 1) to move back to the beginning.

`/` lets you search through the file (case-sensitive). You can then press `n` to navigate to the next match, or `N` to navigate to the previous match.

### Grepping

`grep` is case-sensitive by default.

```
$ grep rose sonnets.txt | wc
   10   82   419
$ grep -i rose sonnets.txt | wc
   12   96   508
$ grep Rose sonnets.txt | wc
   3		22	 130
$ grep Rose sonnets.txt | grep -v rose | wc
   2    14   89
```

*grep* stands for “**g**lobally search a **r**egular **e**xpression and **p**rint.”

```
$ grep -n " ro[a-z]*s " sonnets.txt 
597:  To that sweet thief which sourly robs from me.
917:Die to themselves. Sweet roses do not so;
1100:When rocks impregnable are not so stout,
1339:He robs thee of, and pays it thee again.
1679:The roses fearfully on thorns did stand,
2202:I have seen roses damask'd, red and white,
2203:But no such roses see I in her cheeks;
```

one of the best tool for learning how to use regexes is an online regex builder, such as regex101. Unfortunately, `grep` often doesn’t support the precise format used by regex builders

**Grepping processes**

the `top` command shows the processes consuming the most resources.

the way to see all the processes is to use the `ps` command with the `aux` options:

```
$ ps aux | grep spring
 ubuntu 12241 0.3 0.5 589960 178416 ? Ssl Sep20 1:46
 spring app | sample_app | started 7 hours ago
```

the first number is the *process id*, or pid (often pronounced to rhyme with “kid”).

```
$ kill -15 12241
```

This is the technique for killing individual processes, but sometimes it’s convenient to kill all the processes matching a particular process name:

```
$ pkill -15 -f spring
```

The `history` command prints the history of commands in a particular terminal shell. One use of `history` is to grep your commands to find useful ones you’ve used before. `!n` executes command number `n`.

## Directories

### Directory structure

tasks executed as `root` should typically use the `sudo` command.

### Making directories

```
$ mkdir text_files
$ mv *.txt text_files/
$ ls -ld text_files/
drwxr-xr-x 7 mhartl staff 238 Jul 24 18:07 text_files
$ cd text_files/
$ pwd
/Users/mhartl/text_files
```

`-p` makes intermediate directories as required.

### Navigating directories

```
$ cd
$ pwd
/Users/mhartl
$ find . -name '*.txt'
./text_files/sonnet_1.txt
./text_files/sonnet_1_reversed.txt
./text_files/sonnets.txt
```

The `find` utility is incredibly useful for finding a misplaced file at the command line.

```
$ cd ~/ruby/projects
$ open .
```

The  `open` command opens its argument using whatever the default program is for the given file or directory.

`cd -` cds to the *previous* directory. `cd -` is especially useful when combining commands,

**Combining commands**

commands separated by `&&` run only if the previous command *succeeded*.

### Renaming, copying, and deleting directories

```
$ rm -rf second_directory/
```

#### Grep redux

As with `cp` and `rm`, `grep` takes a “recursive” option, `-r`, which greps through a directory’s files and the files in its subdirectories

