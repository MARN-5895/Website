# Assignment 3: Improving the course Web site through a Pull Request on Github
In [Lecture 3](../../lectures/03_gitandgithub/README.md) we introduced git and Github for tracking changes to code (simple text files). This assignment will help you learn more about git and Github, specifically about how to collaborate on a coding project by forking and cloning a repository, creating a new branch for making and testing changes, and then submitting a pull request to merge those changes into the main repository. We will do that using the course Web site hosted on Github. **Most serious coding projects use a development workflow similar to what you will learn in this assignment.** Even Github used to used a similar workflow (but without forks) to [develop Github](https://www.youtube.com/watch?v=qyz3jkOBbQY).

## Step 1: Set up git on your local computer

Since Storrs HPC is down today, we have to work on our local laptops. All you need today is a terminal. On Windows, you can use Git Bash for Windows; on MacOS you can use the default Terminal application.

Following the set up commands learned in [Lecture 3](../../lectures/03_gitandgithub/README.md), set up `git` on your local computer. Make sure you have an SSH key pair generated on your local computer and connected to Github.

Now create a directory for this assignment. Your directory should be named `03` and should be inside a directory named `Assignments`, which should be inside a directory for the MARN5895 course (a directory tree similar to the one we created on Storrs HPC). 

## Step 2: Fork the course's Github repository from Cesar's Github account

Visit MARN5895's repository hosted on Cesar's Github profile:

https://github.com/cesar-rocha/MARN-5895

"Fork" the repository by clicking on `fork` in the upper-right corner. Forking someone else's repository means copying it to your Github account. Now that you have your fork, you can move on to

---
Exercise: Revise your assigned lecture/assignment notes

1. Clone your forked MARN-5895 repository. Hint: use `git clone git@github.com:USER-NAME/MARN-5895.git`.
2. Set your fork to track the original reposiroty (aka upstream). Hint: use `git remote add upstream git@github.com:cesar-rocha/MARN-5895.git`.
2. Create new git branch with where you will make changes to the orignal content, e.g.: `git checkout -b fix_typos`
3. Revise your assigned lecture or assignment section using a text editor (Visual Studio Code, nano, vi).
4. Commit your changes with meaning commit messages.
---

## Step 3: Submit a Pull Request 
You should now send your changes back to Github and propose to merge your branch into the original repository (cesar-rocha/MARN-5895). 

---
Exercise: push your changes to Github and submit a pull request

1. Push your new branch to your forked Github repository, e.g.: `git push origin fix_typos`
2. Visit your forked repository on Github and submit a pull request (PR) on Github to merge your changes to the original repository on Cesar's profile. (You should see a green buttom "Compare & Merge"). Your PR should contain a short description of what changes you made to the files (e.g., fixed typos and improved wording in section Step 1 of Assignment 1). 
3. Using the option on the menu on the right of you PR, assign your pair to review the PR.
4. Review the PR of your pair. You should click on the commit to check what changes your pair has made and make a comment on the PR.
---

**Notify Cesar that you completed Step 3. HE will review your PR, accept your changes and merge your branch into the master branch of the original repository.**

## Step 4: Update your fork and local branch
When Cesar accepts your PR, your branch will be merged into the master branch of the orignal upstream repository. You should now update your main branch and delete your `fix_typos` branch. On your terminal, do:

```BASH
git checkout main
git fetch upstream
git rebase upstream/main
git branch -d fix_typos
```

You can now push the changes to your fork:

    git push -u origin main

And you can verify on Github that your fork is up-to-date with the original upstream repository (hosted on Cesar's Github profile).

Congratulations! You just helped Cesar improve the course content. Whenever you identify a few typos or any poorly written section in the course material, please feel free to submit a PR. That would be very much appreciated. *Before making changes to the course Web site, remember to update your fork and local repositories  with `git fetch upstream` and `git rebase upstream/main`, because the MARN-5895 Github repository is updated almost daily during the semester, outdating your fork.*

