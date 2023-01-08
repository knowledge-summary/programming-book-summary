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
  - [Basic Branching and Merging](#basic-branching-and-merging)
    - [Basic merging](#basic-merging)
    - [Basic merge conflicts](#basic-merge-conflicts)
  - [Branch Management](#branch-management)
    - [Branch Management](#branch-management-1)
    - [Changing a branch name](#changing-a-branch-name)
  - [Git Workflow](#git-workflow)
    - [Long-running branches](#long-running-branches)
    - [Topic branches](#topic-branches)
  - [Remote branches](#remote-branches)
    - [Push branch to remote](#push-branch-to-remote)
    - [Fetching branch from remote and work with it](#fetching-branch-from-remote-and-work-with-it)
    - [`git pull`](#git-pull)
    - [Delete a remote branch](#delete-a-remote-branch)
  - [Rebasing](#rebasing)
    - [More complicated rebase](#more-complicated-rebase)
    - [When not to rebase](#when-not-to-rebase)
    - [Rebase when doing `git pull`](#rebase-when-doing-git-pull)
    - [Commit History](#commit-history)
- [Git on the Servers](#git-on-the-servers)
- [Distributed Git](#distributed-git)
  - [Workflow Type](#workflow-type)
    - [Centralized Workflow](#centralized-workflow)
    - [Integration-Manager Workflow](#integration-manager-workflow)
    - [Dictator and Lieutenants Workflow](#dictator-and-lieutenants-workflow)
  - [Contributing to a Project](#contributing-to-a-project)
  - [Maintaining a Project](#maintaining-a-project)
- [Github](#github)

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

If you are using a HTTPS url to push over, Git will ask for your username and password for authentication. If you want to avoid typing it every single time you push, you can set up a "credential cache".
``` shell
git config --global credential.helper cache
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

`origin` is the default name Git gives to the server you cloned from. You can also set the name using `-o` option.
``` shell
git clone -o booyah https://github.com/schacon/ticgit
```

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

## Basic Branching and Merging
Example of real life workflow
1. Do some work on main branch
2. Create a branch to work on new user story.
3. Receive a call to carry out hotfix for critical issue.
4. Switch back to the production branch.
5. Create a hotfix branch.
6. After the hotfix is tested, merge it to the main branch and push to production.
7. Switch back to the original user story and continue working.

Using the steps in the previous session, you create the user story branch and add new commit.
![](https://git-scm.com/book/en/v2/images/basic-branching-3.png)

Now you receive the call requesting the hotfix, you are switching back to the `master` branch.

Do note that if your working directory or staging area has uncommitted changes that conflicts with the branch you're checking out, Git will return an error. It is best to have a clean working state when you switch branch.
``` shell
git checkout master
```

### Basic merging
Create a hotfix branch and commit the fix.
``` shell
$ git checkout -b hotfix
Switched to a new branch 'hotfix'
$ vim index.html
$ git commit -a -m 'Fix broken email address'
[hotfix 1fb7853] Fix broken email address
 1 file changed, 2 insertions(+)
```
![](https://git-scm.com/book/en/v2/images/basic-branching-4.png)

After the hotfix is tested and work as intended, checkout to the `master` branch and run `git merge` to merge the `hotfix` branch with the `master branch`.

``` shell
$ git checkout master
$ git merge hotfix
Updating f42c576..3a0874c
Fast-forward
 index.html | 2 ++
 1 file changed, 2 insertions(+)
```

You'll notice the phrase "fast-forward" in the merge. Because the commit `C4` pointed to by the branch hotfix you merged in was directly ahead of the commit `C2` you're on, Git simply moves the pointer forward.

when you try to merge one commit with a commit that can be reached by following the first commit’s history, Git simplifies things by moving the pointer forward because there is no divergent work to merge together — this is called a "fast-forward."

![](https://git-scm.com/book/en/v2/images/basic-branching-5.png)

After that, you delete the hotfix branch and switch back to the original user story to continue the work.
``` shell
$ git branch -d hotfix
Deleted branch hotfix (3a0874c).
```

``` shell
$ git checkout iss53
Switched to branch "iss53"
$ vim index.html
$ git commit -a -m 'Finish the new footer [issue 53]'
[iss53 ad82d7a] Finish the new footer [issue 53]
1 file changed, 1 insertion(+)
```

![](https://git-scm.com/book/en/v2/images/basic-branching-6.png)

It is worth noting that the work done in hotfix is not yet applied to your user story branch.

Let say you have completed your user story and it is ready to be merged to the `master` branch. You will do a `git merge`, similar to what you do to the `hotfix` branch. There are several situation that can happen.

``` shell
$ git checkout master
Switched to branch 'master'
$ git merge iss53
Merge made by the 'recursive' strategy.
index.html |    1 +
1 file changed, 1 insertion(+)
```

As the development history has diverged from some older point, the commit on the user story branch is not a direct ancestor of the `master` branch, Git has to do some works. In this case , Git does as simple three-way merge, using the two snapshots pointed to by the branch tips and the common ancestor of the two.

![](https://git-scm.com/book/en/v2/images/basic-merging-1.png)

In this case, Git will create a new snapshot resulted from the three-way merge and automatically create a new commit that points to it. This is referred to as a merge commit.

![](https://git-scm.com/book/en/v2/images/basic-merging-2.png)


### Basic merge conflicts
Ocassionally, this process doesn't go smoothly. This happens when you changed the same part of the same file in two branches you are merging. Git won't be able to handle the merge itself.
``` shell
$ git merge iss53
CONFLICT (add/add): Merge conflict in index.html
Auto-merging index.html
Automatic merge failed; fix conflicts and then commit the result.
```

Git will ask you to resolve the merge conflict. Running `git status` will show the conflicted file.
``` shell
$ git status
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")

Unmerged paths:
  (use "git add <file>..." to mark resolution)

    both modified:      index.html

no changes added to commit (use "git add" and/or "git commit -a")
```

Opening the file that have merge conflict will show a section as follows. Git add standard conflict-resolution markers to the files that have conflicts.
``` shell
<<<<<<< HEAD:index.html
<div id="footer">contact : email.support@github.com</div>
=======
<div id="footer">
 please contact us at support@github.com
</div>
>>>>>>> iss53:index.html
```

This means the version in HEAD is the top part of that block (everything above the =======), while the version in your user story branch looks like everything in the bottom part.

To solve the merge conflict, you can merge the content yourself.
``` shell
<div id="footer">
please contact us at email.support@github.com
</div>
```

After that, run `git add` to mark a file as resolved. If you are happy with the changes, use `git commit` to finalize the merge commit.

`git mergetools` can also be used to fire up an appropriate visual merge tool and walks you through the conflict.

## Branch Management
### Branch Management
Use `git branch` to see the list of branches
``` shell
$ git branch
  iss53
* master 
  testing
```
`*` indicates the current checked out branch.

To see the last commit of each branch, add `-v`
``` shell
$ git branch -v
  iss53 93b412c Fix javascript issue
* master 7a98805 Merge branch 'iss53'
  testing 782fd34 Add scott to the author list in the readme
```

`--merged` and `--no-merged` option can be used to filter the branches that you have and have not yet merged into the branch you're currently on.
``` shell
$ git branch --merged
  iss53
* master
```

``` shell
$ git branch --no-merged
  testing
```
You can also provide a branch name to show the merge state with respect to a certain branch.
``` shell
$ git checkout testing
$ git branch --no-merged master
  topicA
  featureB
```

Because the `testing branch` isn't merged, trying to delete it with `git branch -d` will fail.
``` shell
$ git branch -d testing
error: The branch 'testing' is not fully merged.
If you are sure you want to delete it, run 'git branch -D testing'.
```
Git message shows that you can force delete the branch using `-D` option.

### Changing a branch name
Suppose you name a branch inappropriately and want to change the name from `bad-name` to `good-name`.

Rename the branch locally with the `git branch --move`
``` shell
git branch --move bad-name good-name
```

The branch name is changed but only locally, to show it in the remote, push it.
``` shell
git push --set-upstream origin good-name
```

``` shell
$ git branch --all
* good-name
  main
  remotes/origin/bad-name
  remotes/origin/good-name
  remotes/origin/main
```

The `good-name` branch is in remote now. However, notice that the `bad-name` is still present in remote too, you can delete it.
``` shell
git push origin --delete bad-name
```

If you are renaming an important branch, before deleting the old branch remotely, make sure to work with the collaborators to update the code, configuration , build scripts, documentation and close the pull requests to the old branch.

## Git Workflow
### Long-running branches
Many Git developer have a workflow that embraces the approach of having several branches that are long lived and used for different stages of development cycle.
![](https://git-scm.com/book/en/v2/images/lr-branches-2.png)

An example is having the stable and production ready code on `master` branch, and having another branch called `develop` or `next` that the developer works on and merge to `master` branch once it is stable. Some larger projects might have more long-running branches such as a `proposed` or `pu` branch. 

### Topic branches
Topic branches is a short-lived branch that are used for a single particular feature or related work. You did a few commits on them, merge them to the long-running branches, and delete them.

Topic branches allow you to switch context quickly and completely. Your work is separated and you can compare them easily.

![](https://git-scm.com/book/en/v2/images/topic-branches-1.png)
![](https://git-scm.com/book/en/v2/images/topic-branches-2.png)

## Remote branches
Remote-tracking branch are references to the state of remote branches. It takes the form `<remote>/<branch>`. For example, when you `git clone`, you will have a local `master` branch and also the tracking branch `origin/master` locally.

The branch that the tracking branch is tracking is called "upstream branch". Tracking branches have a direct relationship with the remote branch, and it will support Git remote server related commands, such as `git pull`.

![](https://git-scm.com/book/en/v2/images/remote-branches-1.png)

The commit history in remote server, local `origin/master` branch and `master` branch can diverge.

![](https://git-scm.com/book/en/v2/images/remote-branches-2.png)

To synchronize the work with a given remote, run `git fetch <remote>` command (`git fetch origin`). This command will fetch the changes from the remote server, update the local database and move your `origin/master` pointer to the up-to-date position.

![](https://git-scm.com/book/en/v2/images/remote-branches-3.png)

You can have multiple remote server, they will be show at `<remote>/<branch>`.
![](https://git-scm.com/book/en/v2/images/remote-branches-5.png)

### Push branch to remote
You have to explicitly push the branches you want to share. If you have a branch name `serverfix` that you want to share. You can push it using `git push <remote> <branch>`. 
``` shell
git push origin serverfix
```

In the background, Git will expand the branch name `serverfix` to `refs/heads/serverfix:refs/heads/serverfix`.

You can also do a more explicit command.
``` shell
git push origin serverfix:serverfix
```

Or if you are using a different branch name in the remote branch. For example, naming the remote branch as `awesomebranch`.
``` shell
git push origin serverfix:awesomebranch
```

### Fetching branch from remote and work with it
When your collaborators fetch from the server, they will get a reference to the remote server `serverfix` under the remote branch `origin/server`. By default, they will not have the local `serverfix` branch.
``` shell
$ git fetch origin
remote: Counting objects: 7, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 3 (delta 0)
Unpacking objects: 100% (3/3), done.
From https://github.com/schacon/simplegit
 * [new branch]      serverfix    -> origin/serverfix
```

To get a local `serverfix` branch, they can run
``` shell
$ git checkout -b serverfix origin/serverfix
Branch serverfix set up to track remote branch serverfix from origin.
Switched to a new branch 'serverfix'
```

If they want a different local branch name, they can set a different branch name.
``` shell
$ git checkout -b sf origin/serverfix
Branch sf set up to track remote branch serverfix from origin.
Switched to a new branch 'sf'
```

They can also use the `--track` shorthand which will set the local branch name the same as the remote branch name
``` shell
$ git checkout --track origin/serverfix
Branch serverfix set up to track remote branch serverfix from origin.
Switched to a new branch 'serverfix'
```

There is an even simple shortcut, if the branch name either doesn't exist locally or exactly matches a name on only one remote.
``` shell
$ git checkout serverfix
Branch serverfix set up to track remote branch serverfix from origin.
Switched to a new branch 'serverfix'
```

If the collaborators already have a local branch and want to set it to the remote branch, or want to change the upstream branch. Use `-u` or `--set-upstream-to` option to `git branch` to explicitly set it.
``` shell
$ git branch -u origin/serverfix
Branch serverfix set up to track remote branch serverfix from origin.
```

After a tracking branch is set up, it can be refer to as `@{u}` or `@{upstream}`. For example, `git merge origin/master` can be written as `git merge @{u}`. It will show if the local branch is ahead, behind or both.

To see the local branch and their tracking branch, you can use the `-vv` option to `git branch`.
``` shell
$ git branch -vv
  iss53     7e424c3 [origin/iss53: ahead 2] Add forgotten brackets
  master    1ae2a45 [origin/master] Deploy index fix
* serverfix f8674d9 [teamone/server-fix-good: ahead 3, behind 1] This should do it
  testing   5ea463a Try something new
```

Do note that the local tracking branch show the commit since the last time you fetched from the remote server. Remember to `git fetch` if you need the up-to-date commit.

### `git pull`
There is a command called `git pull` which is essentially a `git fetch` immediately followed by a `git merge` in most cases.

Generally, it is better to simply use `git fetch` and `git merge` commands explicitly as the magic of `git pull` can be confusing.

### Delete a remote branch
``` shell
$ git push origin --delete serverfix
To https://github.com/schacon/simplegit
 - [deleted]         serverfix
```
The Git server will generally keep the data there for a while until a garbage collection runs.

## Rebasing
In Git, there are 2 ways to integrate changes from one branch into another, the `merge` and the `rebase`.

When there is a diverged work
![](https://git-scm.com/book/en/v2/images/basic-rebase-1.png)

Doing a merge will result as follows
![](https://git-scm.com/book/en/v2/images/basic-rebase-2.png)

If you do a rebase, it will take the change from `C4` and reapply on top of `C3`.
``` shell
$ git checkout experiment
$ git rebase master
First, rewinding head to replay your work on top of it...
Applying: added staged command
```
![](https://git-scm.com/book/en/v2/images/basic-rebase-3.png)

In the background, Git goes to the common ancestor of the two branches (the one you’re on and the one you’re rebasing onto), getting the diff introduced by each commit of the branch you’re on, saving those diffs to temporary files, resetting the current branch to the same commit as the branch you are rebasing onto, and finally applying each change in turn.

After that, you can go back to the master to do a fast-forward merge.
``` shell
$ git checkout master
$ git merge experiment
```
![](https://git-scm.com/book/en/v2/images/basic-rebase-4.png)

Rebase helps to make the commit history clean, as it looks like a linear history now. 

### More complicated rebase
Let say your commit history looks as follows
![](https://git-scm.com/book/en/v2/images/interesting-rebase-1.png)

You decided to merge the `client` branch changes into the main branch for release, but keep the `server` branch changes. `master` branch is not the direct parent branch of `client` branch. Hence, you can use `--onto` to change the parents. `git rebase --onto <newparent> <oldparent> <branch>`.
``` shell
git rebase --onto master server client
```
![](https://git-scm.com/book/en/v2/images/interesting-rebase-2.png)

Now, you can fast-forward your `master` branch.
``` shell
$ git checkout master
$ git merge client
```
![](https://git-scm.com/book/en/v2/images/interesting-rebase-3.png)

You can then rebase the `server` branch into `master` branch and do a fast forward merge.
``` shell
git rebase master server
```
![](https://git-scm.com/book/en/v2/images/interesting-rebase-4.png)

``` shell
$ git checkout master
$ git merge server
```
Delete the branches
``` shell
$ git branch -d client
$ git branch -d server
```
![](https://git-scm.com/book/en/v2/images/interesting-rebase-5.png)

### When not to rebase
**Do not rebase commits that exist outside your repository and that people may have based work on.**

When you rebase stuff, you’re abandoning existing commits and creating new ones that are similar but different. It will cause trouble to others who based their work on the existing commits.

Although it is not advisable to do it, Git have some magic that can help. Git calculates a checksum that is based just on the patch introduced with the commit. This is called a "patch-id". Therefore, it can often successfully figure out what is unqiuely yours and complete the rebase.

### Rebase when doing `git pull`
To apply `git rebase` instead of `git merge` when running `git pull`. Run`git pull --rebase`, or use `git fetch` followed by `git rebase`.

For `git pull` to use rebase by default, you can set the pull.rebase config value as true `git config --global pull.rebase true`.

### Commit History
There are different views on commit history.
- Commit history is a record of **what actually happened**.
- Commit history is the **story of how your project was made**.

It is up to the team and project to decide how they want to design the commit message.

To get the best of both worlds, you should rebase local changes before pushing to clean up your work, but never rebase anything that you've push somewhere.


# Git on the Servers


# Distributed Git
The distributed nature of Git allows far more flexible in how developers collaborate on projects. In Git, every developer is potentially a node and a hub, contributing code to other repositories and maintain a public repository which others can base on.

## Workflow Type
### Centralized Workflow
In centralized workflow, one central hub, or *repository* can accept code, and everyone synchronize with the centralized location.
![](https://git-scm.com/book/en/v2/images/centralized_workflow.png)

If two developers clone from the hub and make changes. The first developer can push their change back up with no problems. The second developer must merge the change by the first developer before pushing changes up, so as to not overwrite the first developer's changes.

### Integration-Manager Workflow
In integration-manager workflow, everyone create their own public clone of the project and push changes to it. Each developer has write access to their own public repository and read access to everyone else's. There is usually a canonical repository that represent the official project. 

You can send a request to the maintainer to pull in your changes. The maintainer can then add your repository as remote, test and merge your commit, and push back to the canonical repisitory.

The process works as follows.
1. The project maintainer pushes to their public repository.
2. A contributor clones that repository and makes changes.
3. The contributor pushes to their own public copy.
4. The contributor sends the maintainer an email asking them to pull changes.
5. The maintainer adds the contributor’s repository as a remote and merges locally.
6. The maintainer pushes merged changes to the main repository.

![](https://git-scm.com/book/en/v2/images/integration-manager.png)

The advantage of this method is that each party can work at their own pace, without waiting for the project to incorporate their changes.

### Dictator and Lieutenants Workflow
This is a variant of a multiple repository workflow. It is generally used by huge projects with hundreds of developers (example: Linux kernel). 
- Various integration managers (called *lieutenants*) are in charge of certain parts of the repository
- All the lieutenants have one integration manager (called *benevolent director*)
- Benevolent director pushes from their directory to a *reference repository* which all the collaborators pull from

The process works as follows.
1. Regular developers work on their topic branch and rebase their work on top of master. The master branch is that of the reference repository to which the dictator pushes.
2. Lieutenants merge the developers' topic branches into their master branch.
3. The dictator merges the lieutenants' master branches into the dictator’s master branch.
4. Finally, the dictator pushes that master branch to the reference repository so the other developers can rebase on it.

![](https://git-scm.com/book/en/v2/images/benevolent-dictator.png)

## Contributing to a Project


## Maintaining a Project


# Github



