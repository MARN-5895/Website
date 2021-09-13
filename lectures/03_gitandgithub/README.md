# Lecture 3: Version control with git and Github

![](img/Finaldoc.png)

This optional [video](https://www.youtube.com/watch?v=21Gl97tkbHU) explains what is git and Github and how to get started.

## git

Git is a command-line software that tracks changes in code. Git is now widely used for research software development from simple analysis code to complex climate models. When coupled with an online repository service, such as Github, git becomes a powerful tool for working collaboratively on coding projects. For example, numerical models such as [MOM6](https://github.com/NOAA-GFDL/MOM6) and [MITgcm](https://github.com/MITgcm/MITgcm) are developed on Github, with git as the version control software.


Git is already installed on Storrs HPC, and it is also installed on your
personal computer. Before we begin to explore it, let's first set it up:

    git config --global user.name "First and Last Name"
    git config --global email "Email"

You should use the email address  linked to your Github account. Git will use this
information to identify who made changes to the files its track.       

To begin exploring git, let's create a directory for this lecture:

    cd MARN5895/Lectures/
    mkdir 03
    cd 03/

### Initializing git repository

We will create a directory called `recipes`, where we will add some text files:

    mkdir recipes
    cd recipes

To start using git in a directory, you need to initialize the repository:

    git init

This generates configuration files stored in a hidden `.git` directory:

    ls -a
    ls .git

### Tracking new files
Let's create a new file:

    touch frosting.txt

Touch created an empty file named `frosting.txt`. If we "check the status" of the repository 

    git status

we see that `frosting.txt` is untracked by git. To track it, we simply "add it":

    git add frosting.txt

Now `git status` returns `new file:   frosting.txt`, which means that `frosting.txt` has been added to the tracking system of the git repository `recipes`.
Let's open `frosting.txt` and add some text to it:

```BASH
Ingredients:
 - 1/2 cup butter
 - 2/3 cup cocoa
 - 3 cups powdered sugar
 - 1/3 cup milk
 - 1 teaspoon vanilla extract
```

If we do `git status`, we see that `frosting.txt` appears as an untracked file. We need to add it to the tracking system using `git add`:

    git add frosting.txt

Now `git status` returns `modified: frosting.txt`, recognizing that we made changes to `frosting.txt`.  To see what's been added or removed from `fronsting.txt`, we use `git diff frosting.txt`, which should return 

```BASH
diff --git a/frosting.txt b/frosting.txt
index e69de29..387922e 100644
--- a/frosting.txt
+++ b/frosting.txt
@@ -0,0 +1,6 @@
+Ingredients:
+ - 1/2 cup butter
+ - 2/3 cup cocoa
+ - 3 cups powdered sugar
+ - 1/3 cup milk
+ - 1 teaspoon vanilla extract
```

The message above identifies with a plus sign (+) the lines that were added to `frosting.txt`. If lines were removed, they would be identified with a minus sign (-).

We now need to "stage" the file and "commit" those changes:

    git add frosting.txt
    git commit -m "Added ingredients"

A *commit* is a unique identifier added to the tracking system identifying a change to a file or set of files. Each commit should be tagged with a informative "commit message" that briefly explanins the changes. The message above "Added ingredients" is short and punchy and meaningul, an examplar of a good commit message.


Now `git status` returns `nothing to commit, working directory clean`. Let's make further modifications to `frosting.txt`, adding some directions to our frosting recipe:

```BASH
Directions:
  1. In a medium saucepan, melt butter and stir in cocoa.
  2. Alternately add powdered sugar and milk; beat until light and fluffy.
  3. Stir in vanilla.  If necessary, add a small amount of additional milk.
```

Now `git status` again returns `modified:   frosting.txt`, identifying that we made additional changes to `frosting.txt`. We stage and commit those changes:

    git add frosting.txt
    git commit -m "Add directions"

We can check the frosting.txt commit's log using `git log`:

    git log frosting.txt

which for me returns

```BASH
commit c7506d1b81658e70eedaf9a480fb2a3d33904b96
Author: Cesar B Rocha <rocha.cesarb@protonmail.com>
Date:   Mon Sep 13 11:05:40 2021 -0400

    Add directions

commit 89a70deb00ed4220a0ef9fed89d6d663d01c37d7
Author: Cesar B Rocha <rocha.cesarb@protonmail.com>
Date:   Mon Sep 13 11:05:13 2021 -0400

    Add ingredients

```

`git log` identifies each commit with a unique long strings of character (numbers and letters), author and date, and the commit messages. The full tracking history can be accessed with `git history`:

    git history frosting.txt

If we wish, we can move back to older commits to check previous versions of `frosting.txt`.  First, we need to "track the HEAD", meaning that we need to record the more recent commit: 

    git checkout HEAD frosting.txt

Now let's checkout the commit log:

    git log frosting.txt

We can check that the file now is at the stage of "Add ingredients":

    cat frosting.txt

should return

```BASH
Ingredients:
 - 1/2 cup butter
 - 2/3 cup cocoa
 - 3 cups powdered sugar
 - 1/3 cup milk
 - 1 teaspoon vanilla extract
```

We can of course go back to the most recent commit:

    git checkout master

You can check we are back at the most recent commit with `git log` or you can take a look the `frosting.txt` with `cat`:

    cat frosting.txt


---
EXERCISE: Create a file for a recipe of your choice. 

1. Use the Web to find a recipe of a meal you like.
2. Create a file with the necessary ingredients and start tracking it with git.
3. Add instructions for the recipe, then commit the changes.
4. Verify you successfully tracked the file changes with `git log`.

---

## Github
Github is an internet service for software development with git. It allows users to have remote repositories linked to local repositores, providing a cloud-based platform for storing and tracking changes to code.


To begin working with Github, let's visit github.com and create a new repository:

![](img/newgithubrepo.png)

    git remove -v 

    git remote add origin https://github.com/cesar-rocha/recipes

**You chould change the path above to the path of your repository, which involves your Github username.**

<!-- 
### Raising issues

### Pull requests (PRs) -->

## Key points 

- `git` is a powerful version control used to track changes in code.

- `Github` is an internet service used for collaboration and software development.

- `Github` is also a great tool for backing up, documenting, sharing code.
