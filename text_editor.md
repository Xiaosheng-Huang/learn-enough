## Introduction to text editors

### Editing small files

```
$ cd
$ vim .bash_profile
```

press the `i` key to *insert* text. 

press `ESC` to switch from insertion mode back to normal mode.

the ones to move to the beginning and end of the line are `0` and `$`.

### Saving and quitting files

type `:q!<return>` to quit without saving any changes.

In a computing context, an alias is simply a synonym for a command or set of commands.

```bash
alias get='curl -OL'
```

Write the file and quit using `:wq<return>`.

If you make any mistakes, you can type `ESC` followed by `u` to *undo* any of the previous steps.

The command doesn’t yet work. We need to tell the shell about the updated Bash profile file by “sourcing” it:

```
$ source .bash_profile
```

the `.bash_profile` file is sourced automatically when we open a new terminal tab or window.

### Deleting content

we can delete single characters in normal mode using the `x` command. pressing `dd` to delete one line. To get it back, you can press `p` to “put” the line, which also allows you to simulate copying and pasting one line at a time.

### Editing large files

The commands to move one screen at a time are Ctrl-F (Forward) and Ctrl-B (Backward). To move to the end of the file, we can use `G`, and to move to the beginning we can use `1G`. Finally,  *search* involves typing `/<string>` followed by return, and then press `n` to go to the next match.

## Modern text editors

### Choosing a text editor

go to Atom > Install shell commands to enable the `atom` command at the command line.

### Opening

turning on word wrap via View > Toggle Soft Wrap.

#### Previewing Markdown

Packages > Markdown Preview > Toggle Preview

### Moving

Typing ⌘← and ⌘→ to move to the beginnings and ends of lines, and ⌘↑ and ⌘↓ to move to the top and bottom of the file. ⌥← and ⌥→ to move left and right one *word* at a time. ⌃G to go to a particular line *number*. 

### Selecting text

to click on one location, and then Shift-click on another location to select all the text in between.

#### Selecting a single word

- Double-click the word
- Press ⌘D

#### Selecting a single line

- Press ⌘← (twice) to get to the beginning of line, then press ⇧⌘→ to select to the end of line
- Press ⌘→ to get to the end of line, then press ⇧⌘← (twice) to select to the beginning of line

#### Selecting multiple lines

hitting ⌘← to go to the beginning of the first line and then hitting ⇧↓ repeatedly.

#### Selecting the entire document

Press ⌘A

### Cut, copy, paste

When using ⌘x or ⌘c, the selected text is placed in a *buffer*(temporary memory area).

#### Jumpcut

This app expands the buffer by maintaining more than one entry in the history. You can navigate this expanded buffer using ⌃⌥V (cycle forward) and ⇧⌃⌥V (cycle backward).

### Deleting and undoing

Redo is usually ⇧⌘Z or ⌘Y.

### Saving

```bash
# Customize prompt to show only working directory.
PS1='[\W]\$ '
```

## Advanced text editing

### Writing an executable script

```
$ kill -15 12241
```

Sometimes terminate code `15` isn’t enough, and we need to escalate the level of urgency until the process is well and truly dead.

```
$ mkdir ~/bin
$ cd ~/bin
$ atom ekill
```

The `ekill` script itself starts with a “shebang” line (pronounced “shuh-BANG”):

```bash
#!/bin/bash
```

This line tells our system to use the shell program located in `/bin/bash` to execute the script.

```bash

# Kill a process as safely as possible.
# Tries to kill a process using a series of signals with escalating urgency.
# usage: ekill <pid>

# If the number of argument is less than 1, exit with a usage statement.
if [[ $# -lt 1 ]]; then
  echo "usage: ekill <pid>"
  exit 1
fi

# Assign the process id to the first argument.
pid=$1
kill -15 $pid || kill -2 $pid || kill -1 $pid || kill -9 $pid
```

To add `ekill` to our system, we need to do two things:

1. Make sure the `~/bin` directory is on the system *path*, which is the set of directories where the shell program searches for *executable* scripts.
2. Make the script itself executable.

```
$ echo $PATH
```

```
$ atom ~/.bash_profile
```

```bash
export PATH="~/bin:$PATH"
```

If for any reason `~` doesn’t work for you, it’s worth trying `$HOME` instead.

```
$ source ~/.bash_profile
```

```
$ chmod +x ~/bin/ekill
```

we can verify that the `ekill` script is ready to go using the `which` command:

```
$ which ekill
/Users/mhartl/bin/ekill
$ ekill
usage: ekill <pid>
```

### Editing projects

```
$ get https://source.railstutorial.org/sample_app.zip
$ unzip sample_app.zip
```

#### Global find and replace

we can replace

```
(def) (.*)
```

with

```
$1 $2    # function definition
```

### Customization

install the `minimap` package