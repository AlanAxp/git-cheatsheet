# git cheat sheet (for dummies! 😉)

## Basics

Basic commands in Git that are always important to have on hand

1. In the folder where you have created your project, open a terminal and to start git, just type

```basch
git init
```
2. To add the files you want to the staging area, you must do

```bash
git add <file>
```

To add all in one run instead

```bash
git add .
```

3. Surely there will be files that you do not want to be considered when doing `git add .`, or that are too heavy, in this case you must create a file called `.gitignore`, which will work as follows

```.gitignore

# files
/file_I_want_to_ignore.rs 
/file_I_want_to_ignore2.py

# folders
/folder-I-want-to-ignore/
/folder/I/want/to/ignore/
```

4. If you want to see what files are ready to be added to the local repository, you can do it with

```bash
git status
```

5. When checking you see that everything is correct, it is time to do the commit!!
(the `-m` flag is so you know what the hell you're doing in the commit, your future self will appreciate it)

```bash
git commit -m "Im doing ..."
```

6. This process will be repeated several times as your project evolves. If you want to see how the history of each commit you have made has been, you can do it with

```bash
git log 
```
or in a pretty way like

```bash
git log --oneline
```

## Branchs

Your project will start to grow and at one point you want to modify something or add something that you do not want to break your hard work, or you are afraid that it does not work as it should. Time to create a branch!

To create a branch in which you can make modifications to the project, in which you will have "safe" your other version of the project, you will need to do

```bash
git branch <yourNewBranch>
```

But not so fast cowboy, before doing something stupid you should switch to that new branch, otherwise everything will be lost and the world will end. To switch to the new branch you must do

```bash
git checkout <yourNewBranch>
```

This process can be repeated as many times as you need, and to be able to see all the branches, you just have to write

```bash
git branch
```

And to be jumping between branches like a monkey, you just need to keep using the command

```bash
git checkout <anyBranch>
```

Suppose you blew it, as I am sure it will happen, then you decide to forget that all that happened, and you want to eliminate the branch from your mind and your life.

To delete the branch from your local repository, then you must type

```bash
git branch -d <yourLocalBranch>
```

Suppose that after a few commits on a branch, something stops working, and before thinking about suicide, we can better go back to when everything worked beautifully

In order to go back in time, we will do it with the `checkout` command, in which we will put the hash of the commit to which we want to return

```bash
git checkout <commitId>
```

If you want to see the differences between commits, you can, but you will have to write

```bash
git diff <commitId1> <commitId2>
```

This does not mean that it is ready, now you are only seeing it, so that everything really returns to that point you must write


```bash
git add .
git commit -m "Reverting to <commitId>"
git push
```

In the case that you want to go back to the last commit and you were just looking at the past of your code with no intention of reverting something, you can then go back with

```bash
git checkout master
```

and if you want to go back to the changes of the last commit of a file

```bash
git restore <file>
```

## Merges

If the development of your branch was successful and you want to join it to another that you already have, you can do a merge, and this will be as follows.

1. First checkout the branch to which you want to receive the merge

```bash
git checkout <branchBase>
```

Once you are in the branch, from which you want to receive the merge

```bash
git merge <branchInComming>
```

If you screwed up with the name of a branch, don't worry, you can rename it as

(if you are in the branch you wanna rename)
```bash
git branch -m  <newName>
```
(if you are in another branch)
```bash
git branch -m  <oldName> <newName>
```

## Remote repository

But ... what if your computer explodes alv?

It would be great to have a backup in the cloud ... so now we will use GitHub or GitLab, it will be the same

In the service you want the most, you can create a new repository, which you can clone by copying its URL with

```bash
git clone <remoteRepoLink>
```

In order to upload your commit info to a local repository you should do the following

```bash
git add .
git commit -m "to remote repo alv"
git push -u origin <branch>
```

In this case `origin` will be the name of the remote repository

To download the changes from remote repository you must

```bash
git pulll
```

If you are working on a computer and you delete a file to a repository, when you push it, it will no longer appear. But if you are working from another computer and you want to delete the files that are no longer being tracked by git, you can do

```bash
git clean -fd
```

If you want to update the repository, and you are occupying another computer, or you want to be sure you will be in the last commit, execute

```bash
git fetch  --all
git reset --hard origin/<branchName>
```

If you want to delete a branch and you no longer want it to appear in your remote repo, write this

```bash
git push origin --delete <branchName>
```

If you want to rename a branch that is in a remote repo... Well you can just delete that remote branch and upload the local branch with the new name ...duh!

When you are on another computer, you will not get all the branches that are remote, but of course you will be able to see and interact with them, you just have to do

```git
git remote update origin --prune
git branch -a
```
