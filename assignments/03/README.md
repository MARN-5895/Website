# Assignment 3: Improving the course Web site through a Pull Request on Github
In lecture 3... This assignment will help you learn about how to collaborate on a coding project using git and Github.

## Step 1: Launch a terminal shell on a jupyterlab running on Storrs HPC

Following the set up commands learned in [Lecture 2](../lectures/02/README.md), start a jupyterlab service on Storrs HPC and tunnel it to your local browser.

Now create a directory for this assignment. Your directory should be named `03` and should be inside a directory named `Assignments`, which should be inside the MARN5895 directory you have already created. 

## Step 2: Fork the course's Github repository from Cesar's Github account

Visit MARN5895's repository hosted on Cesar's Github profile:

https://github.com/cesar-rocha/MARN-5895

"Fork" the repository by clicking on `fork` in the upper-right corner. Forking someone else's repository means copying it to your Github profile. You can clone your fork, make changes to the forked repository, and push those changes back to Github.  You can then propose to merge your changes into the original repository (cesar-rocha/MARN-5895). 

---
Exercise: Revise your assigned lecture/assignment notes

1. Clone your forked MARN-5895 repository 
2. Set your fork to track the original reposiroty (akak upstream): `git remote add upstream git://github.com/pyqg/pyqg.git` 
2. Create new git branch with where you will make changes to the orignal content, e.g.: `git checkout -b fix_typos`
3. Revise your assigned lecture or assignment section.
4. Commit your changes.
---

## Step 3: Submit a Pull Request 

---
Exercise: push your changes to Github and submit a pull request

1. Push your new branch to your forked Github repository: `git push origin fix_typos`
2. Visit your forked repository on Github and submit a pull request (PR) on Github to merge your changes to the original repository on Cesar's profile. 
---

Your PR should contain a short description of what changes you made to the files (e.g., fixed typos and improved wording in section Step 1 of Assignment 1). Cesar will review your PR, accept your changes and merge your branch into the master branch of the original repository.

## Step 4: Update your fork and local branch
Once your branch has been merged into the master branch of the orignal upstream repository, you should update your master branch and delete your ... branch.

```BASH
git checkout master
git fetch upstream
git rebase upstream/master
git branch -d cool_new_feature
```

You just helped Cesar improve the course content. Whenever you identify a few typos or any poorly written section in the course material, please feel free to submit a PR. That would be very much appreciated. *Remember to always update your fork and local repositories first with `git fetch upstream` and `git rebase upstream/master`, because the MARN-5895 Github content is updated almost daily during the semester.*

