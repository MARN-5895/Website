# Lecture 2: Jupyter lab and more on the Unix shell  

In this lecture, we will learn how to launch a `jupyterlab` service on Storrs HPC and tunnel it
to our local computer, so that can interact with it through our browsers. This is perhaps the most 
convinient functional way of interacting with remote computers, and it is especially ... for running 
Jupyter Notebooks and Python and R on Storrs HPC.

We will need to terminal windows for making this connection, because we will need to type commands both locally (on our laptops) and on Storrs HPC. You can also open a new terminal tab (`Cmd+t` in MacOS or `Crtl+Shift+t` in Windows) instead of new window. 

STOPPED HERE.

## SSHing into Storrs HPC and booting up jupyterlab 
First, we log into Storrs HPC and request a MARN5895 node following the two-command sequence we learned last week:

1. 
    ssh NetID@login.storrs.hpc.uconn.edu

2.  bash launch_bash_slurm_marn5895.sh

We should always execute `launch_bash_slurm_marn5895.sh` when logging to work on Storrs HPC during this class.

We are now on our assigned Storrs HPC node, and we can boot up `jupyterlab` using

    jupyter-lab --no-browser --ip='*' --port=8888

The `--ip='*'` option allows for connections from an expanded range of addresses, and `8888` is the default port, which we may have to change if the port is busy.

## Tunneling the jupyterlab service into your local browser
You now need to forward the jupyterlab service set up on the Storrs HPC node (say, cn344) through port `8888` into port `8888` of your local machine. (You can use a different local port if you want.)  To do that, we now switch to the second terminal window (or tab), on the our local computer, and generate an SSH "tunnel":

    ssh -X -t -t NetID@login.storrs.hpc.uconn.edu -L 8888:localhost:8888 ssh -X NODE -L 8888:localhost:8888

where NODE is the Storrs HPC node where you set up the `jupyterlab` service (e.g., `cn344`). If the tunnel has been successfully set up, this should log you into Storrs HPC (after prompting you for your password).

## Opening jupyterlab on your local browser

Finally, open your local browser and type `localhost:8888`.  You now have a working jupyterlab running on Storrs HPC that you can iterface with on your local browser. 

Jupyterlab is a web-based integrated development environment (IDE) that allows you to run terminals windows, text editors and jupyter notebooks to develop, test and execute code.  We will use the notebook and text edit often in the future weeks. Today, we will do some further work on the terminal. 
We will begin coding in python next week. For now, let's use the terminal on jupyterlab to continue our forway into the Unix shell.
    
## Navigating the file system 2.0
We start by checking our current directory:

    pwd

which should return `/home/NetID`, unless you moved around. If you did, please type `cd` to return to you home directory. To create a new directory, use `mkdir` (make directory):

    mkdir MARN5895

If we list what's in this directory `ls MARN5895`, we get an empty list, because we haven't put anything in it yet. Let's `cd` into it an create a new directories and subdirectories:

    cd MARN5895
    mkdir Lectures
    cd Lectures
    mkdir 02
    cd 02

If we now check the current directory with `pwd` we get:

    /home/NetID/MARN5895/Lectures/02/

Let's copy a directory that will be used for this lecture and for assignment 2 into this current directory. If we try

    cp  /shared/marn5895/data/data-shell .

we get an error: "cp: omitting directory `/shared/marn5895/data/data-shell`". That's because 
`data-shell` in `/shared/marn5895/data/` is not a single file but a directory. To copy directory 
(and all its contents, including files and subdirectories), we need to add the option `-r` to `cp`:

    cp -r /shared/marn5895/data/data-shell .

If we now `ls`, we see that the directory `data-shell` was copied into our current directory. We can move into this directory and check what's in it:

    cd data-shell
    ls

That's Nelle's directory tree. Nelle is a ficticious PhD student created by Software Carpentry to teach the Unix shell. Nelle's directory contains several subdirectories (creatures, data, molecules, north-pacific-gyre, writing) and a couple of files (notes.txt, pizza.cfg, solar.pdf).

Let's see what's in `notes.txt`. We can do this with a few different commands. For example, `cat` (concatenate) will print all content of the file into the screen:

```BASH
- finish experiments
- write thesis
- get post-doc position (pref. with Dr. Horrible)
```

Sounds like a plan. Let's see what Nelle has in `creatures`

    cd creatures
    ls 

She has some data on two legendary creatures: basilisk and unicorn. If we concatenate `basilisk.dat` we get what is lookslike its genetic sequence. A better way to  look at these data is to use the commands `more` or `less`, which will initially print only a number of lines to the screen (more lines in `more`, less in `less`) and let us scroll down the output using the space bar:

    more basilisk.dat

To display just the first few lines a text file, we use the command `head`. For example, to show only the first 3 lines of `basilisk.dat`, we do

    head -n 3 basilisk.dat

Similarly, to display the last few lines of a text file we use the command `tail`, e.g.:

    tail -n 10 basilisk.dat

shows the last 10 lines of `basilisk.dat`.


Let's check what else Nelle has in her directory tree. If we check our currently directory with `pwd` we see that we are in

    /home/NetID/MARN5895/Lectures/02/data-shell/creatures

To go one directory upwards (i.e., back into data-shell) we simply do 

    cd ..

If we `pwd` or `ls` again, we verify that we are in `data-shell/`.

##  A few more commands to deal with text files

Let's move into the `molecules` directory. While we could do this with two separate commands (`cd ..`, then `cd moledules`), it's easiest to use a single command by providing the path of where we want to go (one level upward, then into molecules)

    cd ../moledules

Let's see what inside

    ls

returns

    cubane.pdb    ethane.pdb    methane.pdb
    octane.pdb    pentane.pdb   propane.pdb

Let's take a look what is in one of those files:

    more cubate.pdb

which returns some data about cubane:

```BASH
COMPND      CUBANE
AUTHOR      DAVE WOODCOCK  95 12 06
ATOM      1  C           1       0.789  -0.852   0.504  1.00  0.00
ATOM      2  C           1      -0.161  -1.104  -0.624  1.00  0.00
ATOM      3  C           1      -1.262  -0.440   0.160  1.00  0.00
ATOM      4  C           1      -0.289  -0.202   1.284  1.00  0.00
ATOM      5  C           1       1.203   0.513  -0.094  1.00  0.00
ATOM      6  C           1       0.099   1.184   0.694  1.00  0.00
ATOM      7  C           1      -0.885   0.959  -0.460  1.00  0.00
ATOM      8  C           1       0.236   0.283  -1.269  1.00  0.00
ATOM      9  H           1       1.410  -1.631   0.942  1.00  0.00
ATOM     10  H           1      -0.262  -2.112  -1.024  1.00  0.00
ATOM     11  H           1      -2.224  -0.925   0.328  1.00  0.00
ATOM     12  H           1      -0.468  -0.501   2.315  1.00  0.00
ATOM     13  H           1       2.224   0.892  -0.134  1.00  0.00
ATOM     14  H           1       0.240   2.112   1.251  1.00  0.00
ATOM     15  H           1      -1.565   1.730  -0.831  1.00  0.00
ATOM     16  H           1       0.472   0.494  -2.315  1.00  0.00
TER      17              1
END
```

The terminal is a good programs for dealing with text files. For example, to compute of words in a file, use `wc` (word count):

    wc cubane.pdb

which returns

    20  156 1158 cubane.pdb

The first column is the number of lines in `cubane.pdb`, the second columns is the number of words, and the third is the number of bytes in the file. We now this by checking wc's manual with `man wc`. The manual descriptions contains a few options. For example, to print only the number of lines, we use the `-l` option:

    wc -l cubane.pdb

And for displaying only the number of words, we use the the `-w` option. 

To check the number of lines in each file we can use the wildcard `*`:

    wc -l *.pdb

In  this case, `*` is matching all files that end with the extension `.pdb`. The Unix shell created a list of matching filenames ending in `.pdb` and executed the command `wc -l` for each element of that list. 

The default output of any shell command is the screen, but we can change it into a file. For example,

    wc -l *.pdb > number_of_lines.txt

creates a file `number_of_lines.txt` with the output. We can verify this has happened by printing the file contents on the screen:

    cat number_of_lines.txt

which outputs

  20 cubane.pdb
  12 ethane.pdb
   9 methane.pdb
  30 octane.pdb
  21 pentane.pdb
  15 propane.pdb
 107 total

The file `number_of_lines.txt` is ordered in alphabetical order of the molecules. We may instead want to sort the results by the number of lines in each file:

    sort -n number_of_lines.txt

which outputs

   9 methane.pdb
  12 ethane.pdb
  15 propane.pdb
  20 cubane.pdb
  21 pentane.pdb
  30 octane.pdb
  107 total

## Piping a string of commands

A powerful shell tool the pipeline `|`, which allows us to feed the output of one command into another command. For example,

    wc -l *.pdb | sort -n 

outputs the same sorted list we obtained in two steps above:

   9 methane.pdb
  12 ethane.pdb
  15 propane.pdb
  20 cubane.pdb
  21 pentane.pdb
  30 octane.pdb
  107 total

We can pipe as many command as we wish. If we want to print only the first 6 lines of the output above, thus ignoring the line with the total nubmer of lines, we can do

    wc -l *.pdb | sort -n | head -n 6

And of course, we can always print the output into a text file:

    wc -l *.pdb | sort -n | head -n 6 > sorted_number_of_lines.txt

word count, then sort, then put sorted output into sorted_number_of_lines.txt. 

## For loops and bash (shell) scripts

We can also do loops in Unix shell.  For example, if we want to the name of author who analyzed each of the molecules, we can do 

```BASH
for molecule in *.pdb
do 
head -n 2 $molecule | tail -n 1 
done
```
which should output 

```BASH
AUTHOR      DAVE WOODCOCK  95 12 06
AUTHOR      DAVE WOODCOCK  95 12 18
AUTHOR      DAVE WOODCOCK  95 12 18
AUTHOR      DAVE WOODCOCK  96 01 05
AUTHOR      DAVE WOODCOCK  95 12 18
AUTHOR      DAVE WOODCOCK  95  12 18
```
It looks like Dave Woodcock did all the work.


## Key points 

    - The most basic commands to navigate and orgazine the directory tree are: cd (change directory), cp (copy), mv (move), rm (remove), mkdir (make directory).
    - The wildcard `*` in `*.extension` creates a list of all filenames that end in `.extension` on which a command can operate.
    - Pipe `|` take the output of one shell command and input it into another.