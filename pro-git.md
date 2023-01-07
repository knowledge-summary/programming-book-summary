# Git

*(based on [Pro Git Book](https://git-scm.com/book/en/v2))*

# Table of Contents
- [Git](#git)
- [Table of Contents](#table-of-contents)
- [Getting Started](#getting-started)
  - [History of Version Control](#history-of-version-control)
  - [History of Git](#history-of-git)
  - [Characteristics of Git](#characteristics-of-git)
  - [The Command Line](#the-command-line)
    - [Installation](#installation)
    - [First time Git Set Up](#first-time-git-set-up)
    - [Getting help](#getting-help)
- [Git Basics](#git-basics)
  - [Initializa a Repository](#initializa-a-repository)
  - [Clone an existing repositories](#clone-an-existing-repositories)
  - [Recording changes to the Repository](#recording-changes-to-the-repository)
    - [Check the status of your files](#check-the-status-of-your-files)
    - [Add a new or modified file to staging area](#add-a-new-or-modified-file-to-staging-area)
    - [`.gitignore` file](#gitignore-file)
    - [Viewing your staged and unstaged changes](#viewing-your-staged-and-unstaged-changes)
    - [Commit the changes](#commit-the-changes)
    - [Removing files](#removing-files)
    - [Move Files](#move-files)
  - [Viewing the Commit History](#viewing-the-commit-history)
  - [Undoing Things](#undoing-things)
    - [Modify latest local commits](#modify-latest-local-commits)
    - [Unstaging a staged file](#unstaging-a-staged-file)
    - [Unmodifying a modified file](#unmodifying-a-modified-file)
    - [Unstaging a staged file and unmodifying a modified file with `git restore`](#unstaging-a-staged-file-and-unmodifying-a-modified-file-with-git-restore)
  - [Working with Remotes](#working-with-remotes)
    - [Showing your remotes](#showing-your-remotes)
    - [Adding remote repositories](#adding-remote-repositories)
    - [Fetching and pulling from your remotes](#fetching-and-pulling-from-your-remotes)
    - [Pushing to your remotes](#pushing-to-your-remotes)
    - [Inspecting a remote](#inspecting-a-remote)
    - [Renaming and removing remote](#renaming-and-removing-remote)
  - [Tagging](#tagging)
    - [Listing your tags](#listing-your-tags)
    - [Creating Tags](#creating-tags)
      - [Tagging old commit](#tagging-old-commit)
    - [Sharing tags](#sharing-tags)
    - [Deleting tags](#deleting-tags)
    - [Check out tags](#check-out-tags)
  - [Git Aliases](#git-aliases)
- [Git Branching](#git-branching)
  - [Understanding the way Git does branching](#understanding-the-way-git-does-branching)
    - [Creating a new branch](#creating-a-new-branch)
    - [Switching to a new branch](#switching-to-a-new-branch)

# Getting Started
## History of Version Control
Version control is a systems that records changes to a file or set of files over time so that you can recall specific version later.

**Local version control systems** 
- Copy files into another directory
- Local VCSs tools that have simple database that kept all the changes to files under revision control (eg: Revision Control System(RCS))

**Centralized version control systems (CVCS)** (such as CVS, Subversion, Perforce) have a single server that contains all the version files, and a number of clients that check out files from that central place. The downsides include the single point of failure.

**Distributed version control systems (DVCS)** (such as Git, Mercurial, Bazaar or Darcs). Client don't just check out the latest snapshot of the files, but rather fully mirror the repository, including its full history. Thus, this client repositories can be copied back up to the server to restore it in the case of server failure.

## History of Git
During the early years of the Linux kernel maintenance (1991-2002), changes to the software were passed around as patches and archived files. 

In 2022, the Linux kernel project began using a proprietary DVCS called BitKeeper.

In 2005, the relationship between the community that developed the Linux kernel and the commercial company that developed BitKeeper broke down, and the tool’s free-of-charge status was revoked. 

Therefore, Linux development community (and in particular Linus Torvalds) develop their own tool based on lesson learnt from using Bitkeeper.

## Characteristics of Git
1. Storing snapshot, instead of the differences

Conceptually, most other systems store information as a list of file-based changes. These other systems (CVS, Subversion, Perforce, Bazaar, and so on) think of the information they store as a set of files and the changes made to each file over time (commonly described as delta-based version control).  

Git thinks of its data more like a series of snapshots of a miniature filesystem.  With Git, every time you commit, or save the state of your project, Git basically takes a picture of what all your files look like at that moment and stores a reference to that snapshot. If the file have not changed, Git stores the link to the previous identical file it has already stored.

2. Nearly every operation is local

Most operations in Git need only local files and resources to operate, generally no information needed from other computers from the network. This enable instantaneous operations and working offline.

3. Git has integrity

Everything in Git is checksummed before it is stored and is then referred to by that checksum. This means that it is impossible to change the content without Git knowing.

The function is built into Git at the lowest levels and is integral to its philosophy. The mechanism that Git uses for this checksumming is called **SHA-1 hash**.  This is a 40-character string composed of hexadecimal characters (0–9 and a–f) and calculated based on the contents of a file or directory structure in Git. Example: `24b9da6552252987aa493b52f8696cd6d3b00373`.

4. Git generally only adds data

After you commit a snapshot into Git, it
is very difficult to lose. This makes using Git a joy because we can experiment without the danger of severely screwing things up.

5. The three states
**PAY ATTENTION**, this is the main thing to remember about Git. Git has three states that your files can reside in: *modified*, *staged* and *committed*.
- *Modified* means that you have changed the file but have not committed it to your database yet.
- *Staged* means that you have marked a file in its current version to go into your next commit snapshot.
- *Commited* means that the data is safely stored in your local database.

This leads us to the three main sections of Git project: the working tree, the staging area and the Git directory.

![](https://git-scm.com/book/en/v2/images/lifecycle.png)

The working tree is a single checkout of one version of the project. These files are pulled out of the compressed database in the Git directory and placed on disk for you to use or modify.

The staging area is a file, generally contained in your Git directory, that stores information about what will go into your next commit. Its technical name in Git parlance is the “index”, but the phrase “staging area” works just as well.

The Git directory is where Git stores the metadata and object database for your project. This is the most important part of Git, and it is what is copied when you clone a repository from another computer.

The basic Git workflow goes something like this:
1. You modify files in your working tree.
2. You selectively stage just those changes you want to be part of your next commit, which adds
only those changes to the staging area.
3. You do a commit, which takes the files as they are in the staging area and stores that snapshot permanently to your Git directory.

## The Command Line
### Installation
**Linux**  
- Fedora, RPM-based distribution
``` shell
sudo dnf install git
```

- Debina-based distribution
``` shell
sudo apt install git
```

**MacOS**  
Xcode CLI tool will prompt you to install git if it is not installed
``` shell
git --version
```
Else, you can use homebrew
``` shell
brew install git
```

**Windows**  
Download the installer from [git website](https://git-scm.com/download/win) or use winget
``` shell
winget install --id Git.Git -e --source winget
```

Please refer to [git documentation](https://git-scm.com/downloads) for other installations.

<br>
You can also install Git from source if you want the latest Git version.

### First time Git Set Up
Use `git config` to get and set configuration variables that control how Git looks and operates. These variables can be stored in three different places.
- `[path]/etc/gitconfig` (System setting `git config --system`)
- `~/.gitconfig` or `~/.config/git/config` (User setting ` git config --global`)
- `.git/config` located in Git directory (Single repository setting `git config --local`)

To view all the settings and where they come from, run
``` shell
git config --list --show-origin
```

Things to set up
1. Identity
``` shell
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
```
Many GUI tools will help guiding the setting of the identity when you first run them.

2. Editor
``` shell
git config --global core.editor emacs
```
Example for Windows
``` shell
git config --global core.editor "'C:/Program Files/Notepad++/notepad++.exe'
-multiInst -notabbar -nosession -noPlugin"
```

3.  Default branch name
``` shell
git config --global init.defaultBranch main
```

To check the value of a git setting
``` shell
git config user.name  # return John Doe
```

### Getting help
``` shell
git help <verb>
git <verb> --help
man git <verb>
```

# Git Basics
## Initializa a Repository 
Go to the project directory using `cd` and run
``` shell
git init
```
This will create a `.git` subdirectory that contain all of your necessary repositories files - a Git repository skeleton.

## Clone an existing repositories
``` shell
git clone <url>
```
``` shell
git clone https://github.com/libgit2/libgit2
```
This will create a directory named `libgit2` and initialize a `.git` directory inside it.

You can specify the project name.
``` shell
git clone https://github.com/libgit2/libgit2 newfilename
```

## Recording changes to the Repository
### Check the status of your files
`git status` shows the different state of each files (Untracked file, Changes not staged for commit, Changes to be commited) and the branch.
``` shell
$ git status
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   docker.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        pro-git.md

nothing added to commit but untracked files present (use "git add" to track)
```

We can also run the short version of `git status`
``` shell
$ git status -s
 M README  # modifed and unstaged file
MM Rakefile  # modified and stage, and then modified again 
A  lib/git.rb  # new file in staging area
M  lib/simplegit.rb  # modified and staged file
?? LICENSE.txt  # new file
```

### Add a new or modified file to staging area
``` shell
git add <pathname>
```
If the pathname is a directory, the command adds all the files in that directory recursively.

``` shell
git add *.c
git add LICENSE
```

`git add` can also be used to mark merge-conflicted files as resolved.

If you modify a file after `git add` and before `git commit`, you need to run `git add` again to stage the modification.

### `.gitignore` file
Often, you'll have files that you don't want Git to automatically add or show as untracked, such as log or data files. You can create a file listing patterns to match them named `.gitignore`.

You can refer to [gitignore github](https://github.com/github/gitignore) for comprehensive list maintained by Github.

``` shell
*.[oa]  # ignore any files end with ".o" or ".a"
*~  # ignore all files whose names end with a tilde (~)
```

`.gitignore` file is helpful to avoid accidentally commit redundant files. The rules for the patterns in `.gitignore` file are
- Blank lines and lines started with `#` are ignored
- Standard glob patterns work, and will be applied recursively throughout the entire working tree
- Start patterns with forward slash (`/`) to avoid recursivity
- End patterns with forward slash (`/`) to specify a directory
- Negate a pattern by starting with exclamation point (`!`)

Glob patterns are like simplified regular expression that shells use.
- Asterick (`*`) matches zero or more characters
- [abc] matches any characters inside the brackets (in this case a, b, c)
- Question mark (`?`) matches a single character
- Bracket enclosing characters separated by a hyphen (eg: `[0-9]`) matches any characters between them (in this case 0 through 9)
- Two astericks match nested directories (eg: `a/**/z` would match `a/z`, `a/b/c/z`)

Example from the book
``` shell
# ignore all .a files
*.a

# but do track lib.a, even though you're ignoring .a files above
!lib.a

# only ignore the TODO file in the current directory, not subdir/TODO
/TODO

# ignore all files in any directory named build
build/

# ignore doc/notes.txt, but not doc/server/arch.txt
doc/*.txt

# ignore all .pdf files in the doc/ directory and any of its subdirectories
doc/**/*.pdf
```

### Viewing your staged and unstaged changes
To see which line are changed but not yet staged, run
``` shell
git diff
```

To see which line what have been staged but not commited, run
``` shell
git diff --staged
git diff --cached  # same
```
Example output
``` shell
diff --git a/README b/README
new file mode 100644
index 0000000..03902a1
--- /dev/null
+++ b/README
@@ -0,0 +1 @@
+My Project
```

`git diff` can be viewed in other software like emerge, vimdiff, run `git difftool --tool-help` to see what is available.


### Commit the changes
After staging the files to the staging area, you can commit the changes.

``` shell
git commit
```
This will launch your editor of choice, which can be set by `git config --global core.editor` command.

The editor will show the following message.
``` shell

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch main
# Your branch is up to date with 'origin/main'.
#
# Changes to be committed:
#       modified:   README.md
#       new file:   pro-git.md
#
```

Adding `-v` will add the diff message below the git status message.

You can type the commit message in the text editor, then save and quit the text editor to complete the commit. The comment and diff will be automatically stripped out.

Else, you can type the commit message inline with `-m`
``` shell
$ git commit -m "Story 192: Fix benchmark for material"
[main b045aec] Story 192: Fix benchmark for material
 3 files changed, 154 insertions(+), 60 deletions(-)
```

If you want to update all modified tracked files, add an `-a` option.
``` shell
git commit -a -m "Add new benchmark"
```

### Removing files
There are multiple ways to remove files.
- Use `rm` will simply remove the file, but not tracking the removal
``` shell
rm <filename>
git add <filename>
```
- Use `git rm` will remove the file, and track the removal
  ``` shell
  git rm <filename>
  ```
  `git rm` accepts glob patterns
  ``` shell
  git rm log/\*.log
  ```
  ``` shell
   git rm \*~
  ```

  - If you have your file change (for example: modify or `git add` a file), Git have a safety feature to prevent accidental removal of data. Therefore, you need to use `git rm -f`.
    ``` shell
    git add <filename>
    git rm -f <filename>
    ```
  - Use `git rm --cached` if you want to untrack a file, but keep the file in the working directory
    ``` shell
    git rm --cached project.log
    ```

### Move Files
To rename a file
``` shell
git mv file_from file_to
```

This is equivalent to running
``` shell
mv README.md README
git rm README.md
git add README
```

## Viewing the Commit History
``` shell
$ git log
commit cc48a3446b784b8d886e98c92826999771ad578c (HEAD -> main, origin/main)
Author: wavetitan <wavetitango@gmail.com>
Date:   Mon Dec 19 23:30:14 2022 +0800

    Last Sync: 2022-12-19 23:30:14

commit 82b6dbe2c54fcd16439d6a3724c55330a2f0ac0d
Author: wavetitan <wavetitango@gmail.com>
Date:   Sun Dec 18 23:38:07 2022 +0800

    Initial commit
```
By default, with no arguments, `git log` lists the commits made in that repository in reverse chronological order.

`git log` accepts the following options
- `-p`, `--patch` - show the `git diff` introduced in each commit
- `-<n>` - show the last n entries of commits
- `--stat` - show statistics for files modified in each commit
  ``` shell
  README | 6 ++++++
  Rakefile | 23 +++++++++++++++++++++++
  lib/simplegit.rb | 25 +++++++++++++++++++++++++
  3 files changed, 54 insertions(+)
  ```
- `--pretty` (eg: `--pretty=oneline`) - change the format of the log output
  ``` shell
  $ git log --pretty=oneline
  ca82a6dff817ec66f44342007202690a93763949 Change version number
  085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7 Remove unnecessary test
  a11bef06a3f659402fe7563abf99ad00de2209e6 Initial commit
  ```
  - `format` allows you to specify the format of the log output
    ``` shell
    $ git log --pretty=format:"%h - %an, %ar : %s"
    ca82a6d - Scott Chacon, 6 years ago : Change version number
    085bb3b - Scott Chacon, 6 years ago : Remove unnecessary test
    a11bef0 - Scott Chacon, 6 years ago : Initial commit
    ```
    You can find the pretty format specifier at [git documentation](https://git-scm.com/docs/pretty-formats)
- `--graph` - show a nice ASCII graph showing the branch and merge history
  ``` shell
  $ git log --pretty=format:"%h %s" --graph
  * 2d3acf9 Ignore errors from SIGCHLD on trap
  * 5e3ee11 Merge branch 'master' of git://github.com/dustin/grit
  |\
  | * 420eac9 Add method for getting the current branch
  * | 30e367c Timeout code and tests
  43
  * | 5a09431 Add timeout protection to grit
  * | e1193f8 Support for heads with slashes in them
  |/
  * d6016bc Require time for xmlschema
  * 11d191e Merge branch 'defunkt' into local
  ```

A few common options
| Option | Description |
| --- | --- |
| `-p` | Show the patch introduced with each commit. |
| `--stat` | Show statistics for files modified in each commit. |
| `--shortstat` | Display only the changed/insertions/deletions line from the --stat command. |
| `--name-only` | Show the list of files modified after the commit information. |
| `--name-status` | Show the list of files affected with added/modified/deleted information as well. |
| `--abbrev-commit` | Show only the first few characters of the SHA-1 checksum instead of all 40. |
| `--relative-date` | Display the date in a relative format (for example, “2 weeks ago”) instead of using the full date format. |
| `--graph` | Display an ASCII graph of the branch and merge history beside the log output. |
| `--pretty` | Show commits in an alternate format. Option values include oneline, short, full, fuller, and format (where you specify your own format). |
| `--oneline` | Shorthand for `--pretty=oneline --abbrev-commit` used together. |

For commit limiting, `git log` accepts the following options
- `--since`, `--until` - Show commit by time (accepts different format `2 years 1 day 3 minutes ago`, `2008-01-15`)
  ``` shell
  git log --since=2.weeks
  ```
- `--author` - filter on a specific author
- `--grep` - search for keywords in a commit message
- `--all-match` - Limit the commits output to ones that match all given `--grep`
- `-S <string>` (referred as pickaxe option) - take a string and shows only commits that changed the number of occurences of that string.
  ``` shell
  git log -S function_name  # Check the last commit that add or remove reference to this function_name
  ```
- Path - Limit the log output to commits that introduced a change to these files. Usually preceded by a `--` to separate the paths from the options.
  ``` shell
   git log -- path/to/file
  ```
- `--no-merges` - remove merge commits

A few common options to limit the output of `git log`
| Option | Description |
| --- | --- |
| `-<n>` | Show only the last n commits |
| `--since`, `--after` | Limit the commits to those made after the specified date. |
| `--until`, `--before` | Limit the commits to those made before the specified date. |
| `--author` | Only show commits in which the author entry matches the specified string. |
| `--committer` | Only show commits in which the committer entry matches the specified string. |
| `--grep` | Only show commits with a commit message containing the string |
| `-S` | Only show commits adding or removing code matching the string |


## Undoing Things
Anything that is commited in Git can almost always be recovered. However, anything that was never committed risk being lost.

### Modify latest local commits
After a local commit, if you find out that you made the mistake of forgetting to add some files or messing up the commit message, you can add the modified files to staging area as usual, and run `git commit --amend`. This will push the old commit out and put the new commit in place.

It will prompt you to the text editor to update the commit message.
``` shell
git commit -m 'Initial commit'
git add forgotten_file
git commit --amend
```

### Unstaging a staged file
If you accidentally `git add` a file that are not supposed to be in the next commit, use `git reset <filename>` to unstaged it.
``` shell
git reset CONTRIBUTING.md
```

### Unmodifying a modified file
If you want to revert the modification you made to a file to the previous commit version. Use `git checkout -- <filename>`
``` shell
git checkout -- CONTRIBUTING.md
```

### Unstaging a staged file and unmodifying a modified file with `git restore`
**Unstaging a staged file**
``` shell
git restore --staged <filename>
```

**Unmodifying a modified file**
``` shell
git restore <filename>
```

## Working with Remotes
Remote repositories are versions of your project that are hosted on the Internet or network somewhere. It allows collaboration on Git project.

### Showing your remotes
``` shell
$ git clone https://github.com/schacon/ticgit
Cloning into 'ticgit'...
remote: Reusing existing pack: 1857, done.
remote: Total 1857 (delta 0), reused 0 (delta 0)
Receiving objects: 100% (1857/1857), 374.35 KiB | 268.00 KiB/s, done.
Resolving deltas: 100% (772/772), done.
Checking connectivity... done.
$ cd ticgit
$ git remote
origin
```
`origin` is the default name Git gives to the server you cloned from.

Specify `-v` will show you the URLs that Git stores for the short name.
``` shell
$ git remote -v
origin	https://github.com/schacon/ticgit (fetch)
origin	https://github.com/schacon/ticgit (push)
```

You can have multiple remotes with different names and URLs.

### Adding remote repositories
``` shell
git remote add <shortname> <url>
```

``` shell
git remote add pb https://github.com/paulboone/ticgit
```

Now, you can use `pb` on the command line in lieu of the whole URL.
``` shell
git fetch pb
```

### Fetching and pulling from your remotes
``` shell
git fetch <remote>
```
The command goes out to the remote project and pulls the data from the remote projects that you don't have yet. With that, you will have **references to all the branches from that remote**, which you can merge in or inspect at any time. Do note that you have to merge it manually into your work when you're ready.

``` shell
git fetch pb
```
Paul's main branch is now accessible locally as `pb/main`.

If your current branch is set up to track a remote branch, you can use `git pull` to automatically fetch and merge the remote branch to your local branch.

You can set the default behaviour when running `git pull` by setting `pull.rebase` variable. `git config --global pull.rebase "false"` is the default behaviour of git (fast-forward if possible, else create a merge commit), while `true` will apply `rebase` when pulling.

### Pushing to your remotes
When you have done your commit and want to share, you have to push it upstream. The command is `git push <remote> <branch>`. To push your `main` branch to `origin` server, run 
``` shell
git push origin main
```

### Inspecting a remote
``` shell
git remote show <remote>
```

``` shell
$ git remote show origin
* remote origin
  Fetch URL: https://github.com/schacon/ticgit
  Push  URL: https://github.com/schacon/ticgit
  HEAD branch: master
  Remote branches:
    master                               tracked
    dev-branch                           tracked
  Local branch configured for 'git pull':
    master merges with remote master
  Local ref configured for 'git push':
    master pushes to master (up to date)
```

### Renaming and removing remote
You can run `git remote rename <shortname> <new-shortname>` to change a remote's shortname
``` shell
git remote rename pb paul
```
This will change all the remote branch name too. What used to be referenced as `pb/main` is now at `paul/main`.

You can run `git remote remove <shortname>` to remove a remote.
``` shell
git remote remove paul
```

## Tagging
Git has the ability to tag specific points in a repository's history as being important. Typically, people use tag to mark release points (`v1.1`, `v1.2` and so on).
### Listing your tags
``` shell
git tag
# equivalent to
git tag -l
```

Search for tags that match a particular pattern.
``` shell
$ git tag -l "v1.8.5*"
v1.8.5
v1.8.5-rc1
...
```

### Creating Tags
Git provides two types of tags: **lightweight** and **annotated**.

A lightweight tag is just a pointer to a specific command. 

An annotated tag is stored as full objects in Git database and contains more information such as tagger name, email, date, tagging message. They're checksummed and can be signed and verified with GNU Privacy Guard (GPG). Therefore, annotated tags are preferred.

To create an annotated tag, the easiest way is to specify `-a` when running `git tag`.
``` shell
git tag -a v1.4 -m "version 1.4"
```
`-m` specifies the tagging message, which is stored with the tag. If it is not specified, editor will be launched which is similar to `git commit`.

You can see the tag data and the commit info using `git show`
``` shell
$ git show v1.4
tag v1.4
Tagger: Ben Straub <ben@straub.cc>
Date:   Sat May 3 20:19:12 2014 -0700

my version 1.4

commit ca82a6dff817ec66f44342007202690a93763949
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Mon Mar 17 21:52:11 2008 -0700

    Change version number
```

To create a lightweight tag, just provide the tag name without additional information `git tag <tagname>`
``` shell
git tag v1.4-lw
```

``` shell
$ git show v1.4-lw
commit ca82a6dff817ec66f44342007202690a93763949
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Mon Mar 17 21:52:11 2008 -0700

    Change version number
```

#### Tagging old commit
Suppose you want to tag specified commit, you can use `git tag -a <tagname> <commmit hash>`.
``` shell
git tag -a v1.2 9fceb02
```

### Sharing tags
By default, `git push` doesn't transfer tags to the remote server. Hence, you need to explicitly push the tags after they are created. It works like sharing remote branch, run `git push origin <tagname>`
``` shell
$ git push origin v1.5
Counting objects: 14, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (12/12), done.
Writing objects: 100% (14/14), 2.05 KiB | 0 bytes/s, done.
Total 14 (delta 3), reused 0 (delta 0)
To git@github.com:schacon/simplegit.git
 * [new tag]         v1.5 -> v1.5
```

If we want to push all tags at once, use `--tags` option. This will push both types of tags.
``` shell
$ git push origin --tags
Counting objects: 1, done.
Writing objects: 100% (1/1), 160 bytes | 0 bytes/s, done.
Total 1 (delta 0), reused 0 (delta 0)
To git@github.com:schacon/simplegit.git
 * [new tag]         v1.4 -> v1.4
 * [new tag]         v1.4-lw -> v1.4-lw
```

To push only the annotated tags, use `--follow-tags` option.

### Deleting tags
Delete tag locally, use `git tag -d <tagname>`.
``` shell
git tag -d v1.4-lw
```

Delete tag on remote server, there are 2 common variations
1. `git push <remote> :refs/tags/<tagname>`
  ``` shell
  $ git push origin :refs/tags/v1.4-lw
  To /git@github.com:schacon/simplegit.git
  - [deleted]         v1.4-lw
  ```
2. `git push origin --delete <tagname>`

### Check out tags
To view the version of files a tag is pointing to, you can run `git checkout <tagname>`. This will put your repository in "detached HEAD" state.

``` shell
$ git checkout v2.0.0
Note: switching to 'v2.0.0'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at 99ada87... Merge pull request #89 from schacon/appendix-final
```

In “detached HEAD” state, if you make changes and then create a commit, the tag will stay the same, but your new commit won’t belong to any branch and will be unreachable, except by the exact commit hash.

Therefore, you will generally want to create a branch
``` shell
$ git checkout -b version2 v2.0.0
Switched to a new branch 'version2'
```

## Git Aliases
If you don't want to type the entire text of some Git commands, you can set up alias using `git config`

``` shell
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
```
This means that typing `git ci` will run `git commit`.

Alias can also be helpful to create commands that are more intuitive.  
Example 1:
``` shell
git config --global alias.unstage 'reset HEAD --'
```

This makes the following commands to be equivalent
``` shell
git unstage fileA
git reset HEAD -- fileA
```

Example 2:
``` shell
git config --global alias.last 'log -1 HEAD'
```

``` shell
$ git last
commit 66938dae3329c7aebe598c2246a8e6af90d04646
Author: Josh Goebel <dreamer3@example.com>
Date:   Tue Aug 26 19:48:51 2008 +0800

    Test for current head

    Signed-off-by: Scott Chacon <schacon@example.com>
```

You can also set up alias for non Git command, by starting the command with `!` character.

``` shell
git config --global alias.visual '!gitk'
```

# Git Branching
Git's branching model is said to be its 'killer feature'. It is incredibly lightweight which makes it nearly instantaneous. Git encourages workflows that branch and merge often. Understanding and mastering this feature can entirely change the way that you develop.

## Understanding the way Git does branching
When making a commit, Git stores a commit object that contains pointer to the snapshot of the content you staged. The commit object contains author's name and email address, commit message, and pointers to the commits or commits that directly came before this commit. (initial commit - no parents, merged commit - multiple parents)

When you stage the files, Git compute the checksum of each file (SHA-1), stores that version in Git repository (Git refers to them as blobs), and adds this checksum into the staging area.

When you create a commit by running `git commit`, Git compute the checksum of each subdirectory, and stores them as a tree object in the Git repository. Git then creates the commit object that has the metadata and a pointer to the tree object.

![](https://git-scm.com/book/en/v2/images/commit-and-tree.png)

When you make changes and commit again, the next commit stores the pointer to the commit that came immediately before it.

![](https://git-scm.com/book/en/v2/images/commits-and-parents.png)

A branch in Git is simply a lightweight movable pointer to one of these commits. Every time you commit, the branch pointer moves forward automatically.

![](https://git-scm.com/book/en/v2/images/branch-and-history.png)

### Creating a new branch
When you create a new branch, Git creates a new pointer to the same commit.
``` shell
git branch testing
```
![](https://git-scm.com/book/en/v2/images/two-branches.png)

Git keeps a special pointer called `HEAD` to identify the branch you are currently on. This behaviour can be observed by running `git log --oneline --decorate`. Do note that --decorate is the default behaviour since Git version 2.13, so it can be left out.
``` shell
$ git log --oneline --decorate
f30ab (HEAD -> master, testing) Add feature #32 - ability to add new formats to the central interface
34ac2 Fix bug #1328 - stack overflow under certain conditions
98ca9 Initial commit
```

### Switching to a new branch
`git branch` only creates the branch and doesn't switch to the branch. To switch to the new branch, run `git checkout <branch-name>`.
``` shell
git checkout testing
```

As it is typical to create a new branch and want to switch to that new branch, this can be done by
``` shell
git checkout -b <newbranchname>
```

This moves `HEAD` to point to the testing branch.
![](https://git-scm.com/book/en/v2/images/head-to-testing.png)

When we make a commit, the `HEAD` branch will move forward, while the other branches will still point to the commit they were on.
``` shell
echo "New message" > test.md
git commit -a -m 'made a change'
```
![](https://git-scm.com/book/en/v2/images/advance-testing.png)

If we switch back to master and make modification
``` shell
git checkout master
```
``` shell
echo "Another message" > test.md
git commit -a -m 'made other change'
```
![](https://git-scm.com/book/en/v2/images/checkout-master.png)
![](https://git-scm.com/book/en/v2/images/advance-master.png)

There will be a divergent history, which can be visualize by running `git log`
``` shell
$ git log --oneline --decorate --graph --all
* c2b9e (HEAD, master) Made other changes
| * 87ab2 (testing) Made a change
|/
* f30ab Add feature #32 - ability to add new formats to the central interface
* 34ac2 Fix bug #1328 - stack overflow under certain conditions
* 98ca9 initial commit of my project
```

Because a branch in Git is actually a simple file that contains the 40 character SHA-1 checksum of the commit it points to, branches are cheap to create and destroy. Creating a new branch is as quick and simple as writing 41 bytes to a file (40 characters and a newline).

Because we’re recording the parents when we commit, finding a proper merge base for merging is automatically done for us and is generally very easy to do. These features help encourage developers to create and use branches often

From Git version 2.23 onwards, you can use `git switch` instead of `git checkout`.
- Switch to an existing branch: `git switch <testing-branch>`.
- Create a new branch and switch to it: `git switch -c <new-branch>`. The `-c` flag stands for create, you can also use the full flag: `--create`.
- Return to your previously checked out branch: `git switch -`.
