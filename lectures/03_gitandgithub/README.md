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

Now `git status` returns `new file:   frosting.txt`, which means that `frosting.txt` has been added to the tracking system of the git repository `recipes`. We can "commit" the first change (file creation):

    git commit -m "Created frosting recipe file"

A *commit* is a unique identifier added to the tracking system identifying a change to a file or set of files. Each commit should be tagged with a informative "commit message" that briefly explanins the changes. The message above "Created frosting recipe file" is short and punchy and meaningul, an examplar of a good commit message.


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

The message above "Added ingredients" is again an examples of a good commit message, short and punchy and meaningful.


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


## Github
Github is an internet service for software development with git. It allows users to have remote repositories linked to local repositores, providing a cloud-based platform for storing and tracking changes to code.


To begin working with Github, let's visit github.com and create a new repository `receips`:

![](img/newgithubrepo.png)

We can now add the the Github repository as a remote (upstream) repository:

    git remote add origin git@github.com:GITHUB-USERNAME/recipes.git

You can verify that this worked using

    git remote -v

which should list the address of the remote repository used to push and fetch information from. Before we can synchronize the files in our local and remote repositories, we need to create a pair of SSH keys. On your Storrs HPC terminal, type:

    ssh-keygen -t ed25519 -C "EMAIL"

where EMAIL is the email address you used to sign up to Github. Type enter three times to generate the keys. This commands creates a public/private key pair that we will provide to Github. **The `-t ed25519` type of key does not work on some Storrs HPC nodes. So we also need to create a basic RSA key pair**:

    ssh-keygen -C "EMAIL"

On Github, click on your avatar on the upper-right corner, then Setting, then SSH and GPG Keys, then New SSH key. Use `Storrs HPC` as the name of the ed25519 key. Now paste the public keys you created on Storrs HPC. To see the public keys, type

    cat ~/.ssh/id_ed25519.pub 

Copy the public key and paste it on the Github SSH key box. Repeat this procedure with the rsa key, calling it `Storrs HPC 2`.

Now that we have SSH key pairs set up, we can "push" the files tracked in our local repository into the remote repository. The first time we are pushing a local repository to Github, we need to create a local main branch and push it to Github:

    git branch -M main
    git push -u origin main

If you are prompted for a login and password, you may need generate a personal access token (see below) and use token as your password.



---
Generating a personal access

You may need to create Github [personal access token](https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token). On Github, click on you avatar on the upper-right corner, then Settings, then Developer Settings, then Personal Access Tokens. Generate a new token, set its experation date. Then select the scope of the token (you can select all boxes). Now copy the token and save it somewhere safe. You will need it to access Github.

----

You can check that `frosting.txt` was pushed to the remote repository on Github. All the information, including changes associated with each commit, is also there.

Instead of using SSH to connect to Github, you could also use HTTPS. This requires that you set your remote host using the https address. On the recipes Github repository, copy the https address from the green button "Code" and set it as the remote repository

    git remote add https://github.com/GIT-USERNAME/recipes.git

You can now proceed to push your files to Github:

    git branch -M main
    git push -u origin main

If prompted for a password, remember to use your personal access token.

---
EXERCISE: Create a file for a recipe of your choice. 

1. Use the Web to find a recipe of a meal you like.
2. Create a file with the necessary ingredients and start tracking it with git.
3. Add instructions for the recipe, then commit the changes.
4. Verify that you successfully tracked the file changes with `git log`.
5. Push the changes to Github.

---

### Extra: cloning your remote repository on a different computer

A convinient perk of maintaining your files on a remote repository is that, besides backing up your code, you can clone its contents on a different computer. To learn how that works, open a new terminal tab or windows on your local computer. Now on your Github repository, click on the green buttom `Code` and copy the code line that start with `git@github`. On your local computer terminal type set up the github global username and email following the commands we used in the beginning of this lecture. You should also create an SSH key for you local computer and add it to Github following the steps described above.

Once your set up is finished, you can "clone" the remote repository to your local computer:

    git clone git@github.com:GITHUB-USERNAME/GITHUB-REPOSITORY.git

Remember to change GITHUB_USERNAME and GITHUB_REPOSITORY with your username and repository names.

You now have a copy of your remote repository on your local computer. You can change add new files or change the existing ones. Let's create a new recipe `chili.txt`:

```BASH
Ingredients:
 - 2 pounds ground beef
 - 2 cloves garlic, chopped
 - One 8-ounce can tomato sauce
 - 2 tablespoons chili powder
 - 1 teaspoon ground cumin
 - 1 teaspoon ground oregano
 - 1 teaspoon salt
 - 1/4 teaspoon cayenne pepper
 - 1/4 cup corn flour
 - One 15-ounce can kidney beans, drained and rinsed
 - One 15-ounce can pinto beans, drained and rinsed
                                                        
Directions:
 1. Brown the ground beef in a large bot and drain off the excess fat.
 2. Add the tomato sauce, chili powder, cumin, oregano, salt, and cayenne.
 3. Stir, then cover and simmer over low heat for one hour.
 4. Mix the corn flour and 1/2 cup water in a small bowl.  Add to chili.
 5. Add the beans and simmer for 10 more minutes.
 ```

We can now add and commit this new recipe:

    git add chili.txt
    git commit -m "Added chili recipe"

Let's now push these changes to Github:

    git push

You can check on Github that the file `chili.txt` has been added. 

Now our repository on Storrs HPC is outdated given the latest changes we made on our local computer. To update it, we go on the Storrs HPC terminal and "pull" the changes from the remote repository:

    git pull

You can now check that `chili.txt` has been fetched and merged into the repository on Storrs HPC.


<!-- 
### Raising issues

### Pull requests (PRs) -->

## Key points 

- `git` is a powerful version control used to track changes in code.

- `Github` is an internet service used for collaboration and software development.

- `Github` is also a great tool for backing up, documenting, sharing code.
