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
|`git ls-files`|list of tracked files|

# Undo Changes

|Command|Description |
|--|--|
|`git reset HEAD <file>`|unstage the file|
|`git checkout -- <file>`|back to the last commit|


# Renaming and Moving:
|Command|Description |
|--|--|
|`git mv <file> <newfile>`|one renaming operation|
|`mv <file> <newfile>`|two operations: deletion and creation|
|`git add -A`|recursively adds files, but also updates any files renamed, moved, or deleted|


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

# Alias
|Command|Description |
|--|--|
|`git config --global alias.<alias_name> <git Command>`|alias for a long Command (storead in `~/.gitconfig` file which can be modified)|

# Ignoring unwanted files and folders
Add unwanted files and folders name to `.gitignore` file.

|Example|Description |
|--|--|
|`myfile.txt`|specific file|
|`*.ext`|file pattern|
|`my-folder/`|folder|

* Note: adding `README.md` does not work. `git` does not ignore readme files even if you add it to `.gitignore`.

# Comparison

* Note: All comparisons are done for files **tracked** by git. If file is not in the list of git tracked files (`git ls-files`), the changes will not be shown.

## |Working Directory| and |Staged Area|
|Command|Description |
|--|--|
|`git diff`|all files changes|
|`git diff <file>`|specific file changes|

## |Working Directory| and |Git Repository|
|Command|Description |
|--|--|
|`git diff HEAD`|changes for all files tracked by git with the last commit|
|`git diff HEAD -- <file>`|changes for `<file>` with the last commit|

## |Staged Area| and |Git Repository|
|Command|Description |
|--|--|
|`git diff --staged HEAD`|changes for all files tracked by git comparison with the last commit|
|`git diff --staged HEAD -- <file>`|changes for `<file>` with the last commit|

## |commit| and |last commit|
|Command|Description |
|--|--|
|`git diff <commit1> <commit2>`|comparison between commit1 and commit2|
|`git diff HEAD <commit1>`|changed compared to the last commit|
|`git diff HEAD HEAD^`|changed compared between last commit (`HEAD`) and the one before it (`HEAD^`)

## |local| and |remote|
|Command|Description |
|--|--|
|`git diff master origin/master`|comparison between local repo (`master`) and remote repo (`origin/master`)|

