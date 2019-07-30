## Getting started

### Installation and setup

to install Git, follow the instructions at “[Getting Started – Installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)”.

After installing Git but before starting a project, we need to perform a couple of one-time setup steps:

```
$ git config --global user.name "Your Name"
$ git config --global user.email your.email@example.com
```

Git stores global configuration settings in `~/.gitconfig`.

The output of `git help` is similar to the man pages.

### Initializing the repo

```
[~]$ mkdir -p repos/website
[~]$ cd repos/website/
[website]$git init
```

the `init` command creates a directory called `.git` that distinguishes a Git repository from a regular directory.

### Our first commit

```
[website (master)]$ touch index.html
[website (master)]$ git add -A
[website (master)]$ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

  new file:   index.html
[website (master)]$ git commit -m "Initialize repository"
[website (master)]$ git log
commit 879392a6bd8dd505f21876869de99d73f40299cc
Author: Michael Hartl <michael@michaelhartl.com>
Date:   Thu Dec 17 20:00:34 2015 -0800

    Initialize repository
```

The hash is often referred to as a “SHA” (pronounced *shah*) because of the acronym for the Secure Hash Algorithm used to generate it.

### Viewing the diff

```
[website (master)]$ echo "hello, world" > index.html
[website (master)]$ git diff
diff --git a/index.html b/index.html
index e69de29..4b5fa63 100644
--- a/index.html
+++ b/index.html
@@ -0,0 +1 @@
+hello, world
[website (master)]$ git commit -am "Add content to index.html"
[master 03aff34] Add content to index.html
 1 file changed, 1 insertion(+)
```

To see the difference between staged changes and the previous version of the repo, use `git diff --staged`.

`git log -p` shows the full diffs represented by each commit.

`git commit --amend` Amend the last commit.

`git show <SHA>`

## Backing up and sharing

### Remote repo

You have to type your password every time you want to push any changes; see the article “[Caching your GitHub password in Git](https://help.github.com/en/articles/caching-your-github-password-in-git)”.

```
[website (master)]$ git push
```

## Intermediate workflow

### Ignoring files

On macOS a common side-effect of using the Finder to open directories is the creation of a file called `.DS_Store`.

the Vim text editor sometimes creates *temporary files* whose names involve appending a tilde `~` to the end of the normal filename.

### Branching and merging

makeing a new branch called about-page and checks it out at the same time:

```
[website (master)]$ git checkout -b about-page
[website (about-page)]$ git diff master
[website (about-page)]$ git checkout master
[website (master)]$ git merge about-page
```

Use the command `git branch -D about-page` to delete the topic branch.

### Recovering from errors

get back to the state of the repository as of the most recent commit (a state known as `HEAD`):

```
[website (master)]$ git checkout -f
```

to check out an earlier version of the repository, use the SHAs from the Git log:

```
[website (master)]$ git checkout 03aff34ec4f9690228e057a4252bcca169a868b4
```

```
[website ((03aff34...))]$ git checkout master
[website (master)]$
```

## Collaborating

### Clone, push, pull

**Settings > Collaborators**

```
$ git clone <clone URL>
```

### Pushing branches

```
[website (master)]$ git checkout -b fix-trademark
[website (fix-trademark)]$ git push -u origin fix-trademark
```

```
[website-copy (master)]$ git branch -a
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/fix-trademark
  remotes/origin/master
[website-copy (master)]$ git checkout fix-trademark
```

### GitHub Pages

*any* repository at GitHub containing static HTML is automatically available as a live website.

create free private repositories at Bitbucket.

### Advanced setup

#### A checkout alias

```
$ git config --global alias.co checkout
```

#### Prompt branches and tab completion

```
$ curl -o ~/.git-prompt.sh       -OL https://cdn.learnenough.com/git-prompt.sh
$ curl -o ~/.git-completion.bash \
>      -OL https://cdn.learnenough.com/git-completion.bash
$ chmod +x ~/.git-prompt.sh
$ chmod +x ~/.git-completion.bash
$ atom ~/.bash_profile
```

Then add the configuration to the bottom of the file.  Also, make sure to delete any other lines starting with `PS1`.

```
# Git configuration
# Branch name in prompt
source ~/.git-prompt.sh
PS1='[\W$(__git_ps1 " (%s)")]\$ '
export PROMPT_COMMAND='echo -ne "\033]0;${PWD/#$HOME/~}\007"'
# Tab completion for branch names
source ~/.git-completion.bash
```

```
$ source ~/.bash_profile
```

