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

⇒ **You need to add this file to the (local) Git database :**
`git add program.py`

If you update your file, you’ll have to add it again to validate the modifications in the git database.

Know that inside your local project directory, there are 2 types of files :

- **Tracked :** files you cloned, added, and modified.
- **Untracked :** files you created locally without adding them to the project.

Use : `git status` or `git status --short` to know if all files are tracked or not.

If you want some files to be ignored by Git without being considered as “Untracked”, create a `.gitignore` file. 
Example of .gitignore file :

```bash
cat .gitignore
> *.[oa]
```

Here, any file ending with .o or .a is ignored by git. 

# 5 - Keeping track of your changes

`git status` is great, but it is quite vague because you can only know which files were modified, not what was modified. 
For that, use `git diff`.