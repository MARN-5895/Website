# Lecture 3: Version control with git and Github

![](img/Finaldoc.png)



This optional [video](https://www.youtube.com/watch?v=21Gl97tkbHU) explains what is git and Github and how to get started.

## git

Git is a command-line software that tracks changes in code. Git is now widely used for software development from simple analysis code to complex climate models. When coupled with an online repository service, such as Github, git is a powerful tool for working collaboratively on coding projects. For example, numerical models such as [MOM6](https://github.com/NOAA-GFDL/MOM6) and [MITgcm](https://github.com/MITgcm/MITgcm) are developed collaboratively on Github, with git as the version control software.


To begin working with git, let's create directory for this lecture:

    cd MARN5895/Lectures/
    mkdir 03
    cd 03/

### Initializing git repository

Now ... We will create a directory called planets, where we will add some text files:

    mkdir recipes
    cd recipes

To start using git in a directory, you need to initialize the repository:

    git init

This generates configuration files stored in a hidden `.git` directory:

    ls -a
    ls .git

### Tracking new files
Let's create a new file:

    nano cappucinno.txt

You add some text, e.g., "A cappucino has equal parts of espresso coffee, milk and foam."

If do `git status` we see that `cappuccino.txt`.

### Creating branches



## Github
Github is an internet service for software development with git. It allows users to have remote repositories linked to local repositores, providing a cloud-based platform for storing and tracking changes to code.

### Raising issues

### Pull requests (PRs)


## In summary: the difference between git and Github


## Key points 

- `git` is a powerful version control used to track changes in code.

- `Github` is an internet service used for collaboration and software development.

- `Github` is also a great tool for backing up, documenting, sharing code.