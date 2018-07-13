# Table of Contents:
<!--ts-->
   * [Table of Contents:](#table-of-contents)
   * [Git Basics](#git-basics)
   * [General](#general)
   * [Undo Changes](#undo-changes)
   * [Renaming and Moving](#renaming-and-moving)
   * [History](#history)
   * [Alias](#alias)
   * [Ignoring unwanted files and folders](#ignoring-unwanted-files-and-folders)
   * [Comparison](#comparison)
      * [Setting vscode as difftool and mergetool](#setting-vscode-as-difftool-and-mergetool)
      * [Working Directory | Staged Area](#working-directory--staged-area)
      * [Working Directory | Git Repository](#working-directory--git-repository)
      * [Staged Area | Git Repository](#staged-area--git-repository)
      * [Commit | Last Commit](#commit--last-commit)
      * [Local | Remote](#local--remote)
   * [Branching and Merging](#branching-and-merging)
   * [Rebasing](#rebasing)
   * [Stashing](#stashing)
      * [multiple stashes](#multiple-stashes)
      * [Stash into a Branch](#stash-into-a-branch)
   * [Tagging](#tagging)
      * [Annotated Tag](#annotated-tag)
      * [Other Commands](#other-commands)

<!-- Added by: ali, at: 2018-07-13T09:45-06:00 -->

<!--te-->

# Git Basics

3 local stage + 1 remote:
1. Working directory
    * may or may not be managed by git, but git is aware of them
2. Staging area - pre-commit holding area
    * git index: a holding area for queueing up changes for the next commit
3. Commit - git repository (history in `.git` folder)
4. Remote repository

|Command|Description |
|--|--|
|`git status`|changes between: \|working directory\|staging area\| repository (`.git` folder)\|Remote|


The git repository:
1. Working directory (`~/projects/my-project`)
2. Repository (`/.git` --> hidden)

[Table of Contents](#table-of-contents)
# General
configurations first:
```
git config --global user.name "username"
git config --global user.email "email"
```

|Command|Description|
|--|--|
|`git log`||
|`git alias`||
|`git init 'foldername to be created'`|shorten commands|
|`ls -al`|see all folders including those starting with `.` (e.g: `.git` folder)

|Command|Description |
|--|--|
|`git commit -am "message"`|add and commit|
|`git commit --amend`|pop up editor to update the last commit message|
|`git ls-files`|list of tracked files|

[Table of Contents](#table-of-contents)
# Undo Changes

|Command|Description |
|--|--|
|`git reset HEAD <file>`|unstage the file|
|`git checkout -- <file>`|back to the last commit|

**Note**: `HEAD` is just a pointer.

[Table of Contents](#table-of-contents)
# Renaming and Moving
|Command|Description |
|--|--|
|`git mv <file> <newfile>`|one renaming operation|
|`mv <file> <newfile>`|two operations: deletion and creation|
|`git add -A`|recursively adds files, but also updates any files renamed, moved, or deleted|

[Table of Contents](#table-of-contents)
# History
|Command|Description |
|--|--|
|`git help log`||
|`git log`||
|`git log --since "2 days ago"`||
|`git log --oneline`|show commits in one line|
|`git log --oneline --graph --decorate `|show commits graph with branches (decorate)|
|`git log --abbrev`|make commit ids abbreviated|
|`git log -- <file>`|logs for a specific file|
|`git show <commit_id>`|history of a specific commit|

[Table of Contents](#table-of-contents)

# Alias
|Command|Description |
|--|--|
|`git config --global alias.<alias_name> <git Command>`|alias for a long Command (storead in `~/.gitconfig` file which can be modified)|

[Table of Contents](#table-of-contents)

# Ignoring unwanted files and folders
Add unwanted files and folders name to `.gitignore` file.

|Example|Description |
|--|--|
|`myfile.txt`|specific file|
|`*.ext`|file pattern|
|`my-folder/`|folder|

* Note: adding `README.md` does not work. `git` does not ignore readme files even if you add it to `.gitignore`.

[Table of Contents](#table-of-contents)

# Comparison
* Note: All comparisons are done for files **tracked** by git. If file is not in the list of git tracked files (`git ls-files`), the changes will not be shown.

[Table of Contents](#table-of-contents)
## Setting vscode as difftool and mergetool
The way to wire them together is to modify your `.gitconfig` and you have two options.

1. To do this with command line entries, enter each of these:
```
git config --global merge.tool vscode
git config --global mergetool.vscode.cmd "code --wait $MERGED"
git config --global diff.tool vscode
git config --global difftool.vscode.cmd "code --wait --diff $LOCAL $REMOTE"
```
2. To do this by pasting some line in the `.gitconfig` with VS Code.

    * Run git `config --global core.editor "code --wait"` from the command line.
    * From here you can enter the command `git config --global -e`. You will want to paste in the code in the "Extra Block" below.
```
[user]
    name = EricDJohnson
    email = cool-email@neat.org

# Comment: You just added this via 'git config --global core.editor "code --wait"'
[code]
    editor = code --wait

# Comment: Start of "Extra Block"
# Comment: This is to unlock VSCode as your git diff and git merge tool    
[merge]
    tool = vscode
[mergetool "vscode"]
    cmd = code --wait $MERGED
[diff]
    tool = vscode
[difftool "vscode"]
    cmd = code --wait --diff $LOCAL $REMOTE
# Comment: End of "Extra Block"
```
Now in your git directory with a conflict, run `git mergetool` and you have `VSCode` helping you handle the merge conflict! To compare, run `git difftool`.

[Table of Contents](#table-of-contents)

## Working Directory | Staged Area
|Command|Description |
|--|--|
|`git diff`|all files changes|
|`git diff <file>`|specific file changes|

[Table of Contents](#table-of-contents)
## Working Directory | Git Repository
|Command|Description |
|--|--|
|`git diff HEAD`|changes for all files tracked by git with the last commit|
|`git diff HEAD -- <file>`|changes for `<file>` with the last commit|

[Table of Contents](#table-of-contents)
## Staged Area | Git Repository
|Command|Description |
|--|--|
|`git diff --staged HEAD`|changes for all files tracked by git comparison with the last commit|
|`git diff --staged HEAD -- <file>`|changes for `<file>` with the last commit|

[Table of Contents](#table-of-contents)
## Commit | Last Commit
|Command|Description |
|--|--|
|`git diff <commit1> <commit2>`|comparison between commit1 and commit2|
|`git diff HEAD <commit1>`|changed compared to the last commit|
|`git diff HEAD HEAD^`|changed compared between last commit (`HEAD`) and the one before it (`HEAD^`)

[Table of Contents](#table-of-contents)

## Local | Remote
|Command|Description |
|--|--|
|`git diff master origin/master`|comparison between local repo (`master`) and remote repo (`origin/master`)|

[Table of Contents](#table-of-contents)

# Branching and Merging
|Command|Description |
|--|--|
|`git branch`|list of all branches|
|`git branch -a`|list of all branches including remotes|
|`git branch <branch>`|making new branch (`<branch>`)|
|`git branch -m <branch> <new_branch>`|renaming branch to new_branch|
|`git checkout <branch>`|switch to branch `<branch>`|
|`git branch -d <branch>`|removing _local_ branch|
|`git push origin --delete <branch>`|removing _remote_ branch|

|Command|Description |
|--|--|
|`git checkout -b <branch>`|make new branch and switch to it|
|`git diff master <branch>`|comparison between two branch|
|`git merge <branch>`|merge branch `<branch>` with the current branch|

**Note**: Fast-forwarded merge means git places all commits on the master branch as if we never branched away. 

Get the graph with `git log --oneline --graph --decorate`:

```
git merge <branch>

  *__*__* new branch
 /                           --->
/ master (no commits here)          /*__*__* master (new branch merged)
```


**Note**: Fast-forwarding is only possible when there are no changes being made on the master branch.


|Command|Description |
|--|--|
|`git merge <branch> --no-ff`|merge branch `<branch>` with the current branch (`master`) **without fast-forwarding**|

Get the graph with `git log --oneline --graph --decorate`:

```
git merge <branch> --no-ff

  *__*__* new branch                  *__*__*
 /                           --->    /       \
/ master (no commits here)          / __ __ __\ master (new branch merged)
```
[Table of Contents](#table-of-contents)

# Rebasing

|Command|Description |
|--|--|
|`git rebase <branch>`|branch is usually the master branch|
```
git rebase <branch>

  *__*__* new branch                           *__*__* new branch
 /                        --->                /       
/ *__*__*__* master               / *__*__*__* master
```
|Command|Description |
|--|--|
|`git rebase --abort`|abort and get back to the state before `git rebase`|
|`git pull rebase`|pull and rebase commits on top of master|

```
git pull rebase

/*__* master                  
                        --->                  
/ *__*__*__* master             / *__*__*__*__*__* master
```

[Table of Contents](#table-of-contents)

# Stashing

|Command|Description |
|--|--|
|`git stash`|stash the current changes|
|`git stash -u`|also include untracked files by git|
|`git stash list`|list of stashes|
|`git stash drop`|drops a stash|
|`git stash apply`|applies the stash on the current branch
|`git stash pop`|`git stash apply` and `git stash drop` in one command|

## multiple stashes
|Command|Description |
|--|--|
|`git stash save "message"`|saves a stash with a message|
|`git stash show stash@{1}`|looks at the second stash|
|`git stash drop stash@{1}`|clears the second stash|
|`git stash clear`|clears all stashes|

**Note**: stashes have index and the last stash index is 0. e.g. 4 saved stashes:
```
stash@{0}
stash@{1}
stash@{2}
stash@{3}
```
`stash@{3}` is the first stash we made and `stash@{0}` is the last stash.

## Stash into a Branch
|Command|Description |
|--|--|
|`git stash branch <branch>`|creates a new branch `<branch>`, stashes into the new branch and drops the stash|

[Table of Contents](#table-of-contents)

# Tagging
|Command|Description |
|--|--|
|`git tag <tag>`|assigns the tag `<tag>` to `HEAD`|
|`git show <tag>`|shows changes of commit to which `<tag>` is assigned.|
|`git tag --list`|shows the list of all tags|
|`git tag --delete <tag>`|removes the tag with name `<tag>`|

## Annotated Tag
Annotated tag is equivalent to a commit message, but for tags.
|Command|Description |
|--|--|
|`git tag -a <tag>`|`-a` means annotated tag. This tag also shows the message assigned to the tag when using `git show <tag>`|
|`git tag -a <tag> -m <message>`|annotated message with message (does not pop up editor for message)|

## Other Commands
|Command|Description |
|--|--|
|`git diff <tag1> <tag2>`|comparing tags|
|`git tag -a <tag> <commit-id>`|tagging a specific commit|
|`git tag -a <tag> -f <commit-id>`|updates the already defined `<tag>` on commit `<commit-id>`|
|`git push origin master <tag>`|pushed the tag to the remote repository|

[Table of Contents](#table-of-contents)