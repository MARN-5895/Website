# Assignment 2: Automating tasks using the Unix terminal

## Step 1: Launch a terminal shell on a jupyterlab running on Storrs HPC

Following the set up commands learned in [Lecture 2](../lectures/02/README.md), set up jupyterlab service and tunnel it to your local browser.

Now start a terminal on `jupyterlab` and navigate into Nelle's North Pacific Gyre directory:

    cd data-shell/north-pacific-gyre/2012-07-03

## Step 2: Add a prefix NPG to all `.txt` files in this directory
This directory contains protein sample data (the `.txt` files) and an analysis script (`goostats.sh`) written by Nelle's advisor. Suppose you want to tag those data filenames with North Pacific Gyre, in case Nelle wants to compare protein sample data across different ocean basins.  You can rename a file using the command `mv` (move). Before attemping to move or rename anything, make a copy of the original data into a new separate sub-directory:

    mkdir original_files
    cp *.txt original_files/

Of course you could do this by hand, one f. But that's too much work, and it is prone to human error. You job is to automate this task using the terminal shell. **Write a shell script that appends the prefix `NPG` (for North Pacific Gyre) to all protein sample data**.

## Step 3: Run shell script `goostats.sh`


## Step 4: Check results?

