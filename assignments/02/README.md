# Assignment 2: Automating tasks using the Unix terminal
Two of the most common basic computational tasks in scientific research are renaming a large number of files and running a script multiple times with different input files. This assignment you help you learn how to use the terminal shell to automate those tasks.

## Step 1: Launch a terminal shell on a jupyterlab running on Storrs HPC

Following the set up commands learned in [Lecture 2](../lectures/02/README.md), start a jupyterlab service on Storrs HPC and tunnel it to your local browser.

Now start a terminal on `jupyterlab` and navigate into Nelle's North Pacific Gyre directory:

    cd MARN5895/Lectures/02/data-shell/north-pacific-gyre/2012-07-03

## Step 2: Add a prefix NPG to all `.txt` files in this directory
This directory contains protein sample data (the `.txt` files) and an analysis script (`goostats.sh`) written by Nelle's advisor. Suppose you want to tag those data filenames with North Pacific Gyre, in case Nelle wants to compare protein sample data across different ocean basins.  You can do that by renaming the files using the command `mv` (move). Before attemping to move or rename anything, make a copy of the original data into a new sub-directory to ensure you won't lose any data if something goes wrong:

    mkdir original_files
    cp *.txt original_files/

You can check that a copy of files exists in `original_files/` using `ls`:

    ls original_files/

Now you can rename the data files. For example, to rename `NENE01729A.txt` and you could do:

    mv NENE01729A.txt NPG_NENE01729A.txt

Of course you could rename the files one by one. But that's too much work, and it is prone to human error. So need to automate this task using the terminal shell. 

---
Exercise: renaming a large number of files

1. Write a shell script that appends the prefix `NPG` (for North Pacific Gyre) to all data filenames. You can name the script `rename_files.sh`. 
2. Run the script in the terminal.
3. Use `ls` to verify all files have been successfully renamed. 
4. Now create a new dictory named `new_files` and move the renamed files into it.
---

## Step 3: Run shell script `goostats`

You are now ready to process Nelle's data  using `goostats.sh`, a shell script written by her advisor. The script calculates some statistics from the protein sample files. To see the contents of it use `cat`:

    cat goostats.sh

which should output 

```BASH
while getopts J:r: option
do
    case "$option" in
    J) Jarg="$OPTARG"
       shift $((OPTIND));;
    r) shift $((OPTIND-1));;
    esac
done

sleep 2
head -3 $1 | cut -d , -f 1 | sort | uniq > $2
```

The details of the script do not matter, but note that it takes two arguments: an input file with the protein data and an output file on which the script will save the statistics. For example, to run `goostats.sh` on `NPG_NENE01729A.txt` you could do:

    bash goostats.sh NPG_NENE01729A.txt stats_output.txt

If you see the contents of `stats_output.txt` you will notice that it contains three numbers (three statistics):

```BASH
0.224455411571
1.03150932862
1.44755225695
```

Note that `stats_output.txt` is not a good filename, because it says nothing about original data that was used to generate the statistics. A better filename would be `stats-NPG_NENE01729A.txt`. To avoid confusion below, delete the `stats_output.txt` file using `rm stats_output.txt`.  

---
Exercise: running a script multiple times with different inputs/outputs

1. Write a shell script that executes goostats.sh for all protein data and save the statistics in properly named output files in a new subdirectory. You should name your script `run_stats.sh` and the output directory should be named `stats`.
2. Execute the script in the terminal.
3. Verify that the script has generated the statistics files in the directory `stats`.

---

## Step 4: Compare scripts and results with other pairs/small groups
Compare and contrats your two bash scripts written to complete steps 2 and 3 with those of your colleagues and reflect on the potentially different approaches to renaming several files and running a script multiple times with different inputs.

