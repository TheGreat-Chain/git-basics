# GUIDE - Git basics

- I decided to write this tutorial while learning to use Git myself, because I think that being able to explain something proves that you understand it deeply.
- As I am a beginner, I’ll certainly make some mistakes. Don’t hesitate to modify or tell me what seems incorrect, in order to make this tutorial relevant.
- If you do not care about the theoretic aspect, skip the first part.

<aside>
💡 Here, you will learn the basics of Git, how it works, the main commands, git branching.

</aside>

- I really suggest you to test the commands on your computer while following this guide.
    
    ### **Have fun !**
    

# 1 - Why is Git so popular ?

## Local operations

While other Version Control Systems rely a lot on the server side which tends to make them slow for certain tasks, **Git gives us the opportunity to work almost exclusively in local.** This makes every operation very fast compared to other VCS.

When your project will reach a stage you want to register, you’ll make a “**commit”.** This action is done locally. It will become public only when you’ll **“push”** your commit. In other words, you can control your versions even when you are working offline. 

## Data Integrity

Let’s say you upload (commit) some files of your program. Let’s say it is the 0.1 version. Then, you will modify your program and commit the new version. 
**Know that the 0.1 version is not lost ! You can rollback to it if you want.** Basically, Git simply adds data, so it is difficult to really lose your information.

We could say many other things, but let’s focus on the practical aspect of Git now !

# 2 - Installation and configuration

## Installation

Since it is really easy, I will just provide you an official link : 
[https://git-scm.com/downloads](https://git-scm.com/downloads)

## Configuration

I think the easiest way is the following :

1. Create an account on : [https://github.com/](https://github.com/)
2. Open Git Bash (on Windows) or your terminal (on Linux)
3. Create a project directory and go in it :  
`mkdir /home/user/myProject ; cd /home/user/myProject`   
4.  Associate this project to your account : 
`git config --global [user.email](http://user.email) [your email]
git config --global [user.name](http://user.name) [your GitHub name]`

And you should be OK.

# 3 - Make or Clone a repository / project

A repository is basically all the files of a project.
You can either create a repository or clone an existing one.

- Create a git repository :
    1. Go in your project directory :
    `cd /home/user/myProject`
    2. Initialize git :
    `git init`
- Clone an existing project :
`git clone [URL] [directory]`
Example : 
`git clone [https://github.com/libgit2/](https://github.com/libgit2/)myProject2`

# 4 - Add files to your project

Let’s say you create a [program.py](http://program.py) file in your project directory. This file exists locally, but Git doesn’t know anything about it yet. 

⇒ **You need to add this file to the staging area :**
`git add program.py`

**Warning :** If you update your file, you’ll have to add it again to update the modifications in the staging area. 

## Some definitions

- **Working directory** : Files on your project directory on your computer.
- **Staging area** : Files tracked by Git after a `git add`.
- **Tracked files** : files in your staging area
- **Untracked files** : files in your working directory but not in your staging area.

Use : `git status` or `git status --short` to know if all files are tracked or not.

If you want some files to be ignored by Git without being considered as “Untracked”, create a `.gitignore` file. 
Example of .gitignore file :

```bash
cat .gitignore
> *.[oa]
```

Here, any file ending with .o or .a is ignored by git. 

# 5 - Keeping track of your changes

- `git status` is great, but it is quite vague because you can only know which files were modified, not what was modified. 
For that, use `git diff`.

## Rollback commands

If you did some things you did not want to do, there is always a solution. These are some “undo” commands :

- `git restore [file]` : In the case you want to remove a file from your staging area.
- `git checkout — [file]` : In the case you want to discard changes made on a file.

# 6 - Commit your changes

## Commit your changes

A commit is a record of your project at this moment. 

`git commit` is used when your staging area is set up the way you want. 
Remember : `git status` to check that.

Most of the time, you’ll add a message with the commit like that :
`git commit -m “Version 0.2”`

## Commit history

You can see the commit history with `git log.`

Some cool options :

- `git log -p` : Shows the differences introduced in each commit
- `git log -s` : to see how many lines were added or deleted in each commit
- `git log --since="1 year 2 months ago"` : to see changes since a relative or absolute date. Useful if you want to limit the log

More about it here : 

[Git - Viewing the Commit History](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History)

# 7 - Collaborating

This is the most interesting and useful part of Git. 
Collaborating with Git involves knowing **remote repositories** management. It means that your local projects will be shared on the Internet or on any network. 

## Create a remote repository on GitHub :

1. Go on “Your profile”
2. Click on “Repositories”
3. Click on “New”

## List of useful commands :

- `git remote -v` : Shows the short name and the URL of the remote servers configured.
- `git remote add [short name] [URL]` : Adds a new remote called [short name]. You’ll refer to this project with the short name and not with the URL.
- `git fetch [remote]` : Gets data from the remote.
- `git pulll [remote]` : Gets data from the remote AND merges with local branches
- `git remote show [remote]` : Shows information about the the remote, mainly about branches.
- `git push [remote] [branch]` : Push your commits on the remote repository.
- `git remote remove [short name]` : Remove a remote.

# 8 - Branching

## What is a branch ?

When you make a commit it creates an identifier and a link to the previous commit. A succession of links is called a branch.

Even if you never use the `git branch` command, all your commits are done on a branch. By default, this branch is called **master.** 

## The master branch

Use `git log --all` to see your commits. 
You’ll obtain something like that :

```
commit 73263f6936859609f54bdac3bd5f2d7c187bbf65 (HEAD -> master)
Author: Login <example@email.com>
Date:   Mon Jan 1 00:00:00 2021 +0100

    version 1.0

commit c83be1422135f463a82e3a87fedf7bc2b771c819
Author: Login <example@email.com>
Date:   Mon Jan 1 00:00:00 2021 +0100

    version 2.0
```

- The strange string after “commit” is its identifier, created with the SHA-1 hashing function.
- On the very first commit (bottom), you do not see any branch information
- On the one above, you can see *“(HEAD → master)”.*

This is important : 

**HEAD** is ****the pointer that indicates on which branch you currently are. In this example, Git considers you currently are on the master branch, the one created and named by default.

## Create your own branches

Use `git branch [branch name]`. 

If you do `git log --all` or (`git log --all --oneline` for more clarity) again :

```
commit 73263f6936859609f54bdac3bd5f2d7c187bbf65 (HEAD -> master, branch)
```

You see that there are now two branches : “master” and “branch” (I called it branch). 
However, you are still on the master branch. 

To move on the other branch, use `git checkout [branch]`. You’ll see the HEAD pointer moving. 

From that point, every commit you’ll make will be only on the branch where the HEAD is pointing. Of course you can move to any branch whenever you want. 

Also, your working directory will only show the files attached to the branch you currently are on. 

## Merge branches

1. Go on the branch you want to keep with `git checkout [branch]`.
2. Do `git merge [branch]` where [branch] is the branch on which you did some work.
3. Delete the branch mentioned in the 2. step with `git branch -d [branch]` because it is no longer useful.
4. Most of the time, same part of same files will be different on two branches because of the modification you did. It is called a conflict. The merging is paused until you resolve the conflict. 
⇒ Use `git status` to help you during this process.