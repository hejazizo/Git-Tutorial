3 local stage + 1 remote:
1. Working directory
    * may or may not be managed by git, but git is aware of them
2. Staging area - pre-commit holding area
    * git index: a holding area for queueing up changes for the next commit
3. Commit - git repository (history in .git folder)
4. Remote repository

git status:
* changes between (1. working directory, 2. staging area, 3. repository (.git folder), 4. Remote)

The git repository:
1. Working directory (~/projects/my-project)
2. Repository (/.git --> hidden)

configurations first:
```
git config --global user.name "username"
git config --global user.email "email"
```

```
git log
git alias  --> shorten commands
git init 'foldername to be created'
ls -al --> see .git folder
```

```
git commit -am "message" --> add and commit
git ls-files --> list of tracked files

```