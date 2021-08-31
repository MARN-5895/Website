# Lesson 1: Introduction to the class, the Unix shell and Storrs HPC

## Welcome to Research Computing in Marine Sciences
Welcome to Research Computing in Marine Sciences! This course will help
you learn modern computing tools for research, with applications in Marine Sciences.
You will learn how to navigate the file system using the terminal, analyze and visualize
data in Python, and work collaboratively using git and Github.

All our work will take on the [Storrs High-Performance Computing](https://hpc.uconn.edu/storrs/cluster-resources/) (HPC) facility.
By now, you should have an account at Storrs HPC and your netID should be linked
to the MARN-5895 class partition. Working on Storrs HPC has the advantage of ensuring
that all students have access to the same computer system and programs, regardless of
the operating system of their personal computer. Plus, you will gain relevant experience
with remote work on a Unix-based supercomputer.

## Getting to know the Unix shell

The Unix shell (aka terminal shell or simply terminal) is a program through
which users interact with computers by typing commands. The shell can be used to
navigate the file system, move files arounds, and run
scripts and complicated programs, such as numerical models.

The easiest way to interact with computers is using a GUI (Graphic User Interface), wherein
we click on programs and folder and drag things around. But the GUI approach is laborious for
complicated (sometimes repetitious) set of actions. That's when the terminal comes in handy. Being
comfortable with the terminal shell will allow you to automate tasks, improve reproducibility of you work,
and access remote computers (including cloud-computing systems).

Learning to use the terminal requires memorizing a few commands. We will use a few of these commands today and
introduce other essential commands as they become necessary to perform your assignments.  


### Linux and MacOS users
Both Linux and MacOS are Unix-based operating systems, and the Unix shell is a
native application. The most common Unix shell application is called `Terminal`.

### Windows users
For Windows users I recommend Git Bash, [Git for Windows](https://gitforwindows.org)'s terminal. You can also use
the terminal that comes with [Visual Studio Code](https://code.visualstudio.com),
a Microsoft text edit that has become the go-to tool for software developers. VSCode
also works on Linux and MacOS.

## Basic commands

To navigate the file system, we use two commands: `ls` (list) and `cd` (change directory). To move files around,
we also use two commands: `cp` (copy) and `mv` (move). These commands also accept optional flags, which modify the
output. For example, `ls` lists the name of files and sub-directories in a specific directory, `ls -l` lists the files
in long-format (showing the size of each file, among other things). I will demonstrate the use of these commands in class and you will
practice their use in an assignment.

To learn about a command syntax and its different options, you can use the
command `man` (manual), for example `man ls` yields

```BASH
LS(1)                     BSD General Commands Manual                    LS(1)

NAME
     ls -- list directory contents

SYNOPSIS
     ls [-ABCFGHLOPRSTUW@abcdefghiklmnopqrstuwx1%] [file ...]

DESCRIPTION
     For each operand that names a file of a type other than directory, ls displays its name as well as any
     requested, associated information.  For each operand that names a file of type directory, ls displays
     the names of files contained within that directory, as well as any requested, associated information.

     If no operands are given, the contents of the current directory are displayed.  If more than one operand
     is given, non-directory operands are displayed first; directory and non-directory operands are sorted
     separately and in lexicographical order.

     The following options are available:

     -@      Display extended attribute keys and sizes in long (-l) output.

     -1      (The numeric digit ``one''.)  Force output to be one entry per line.  This is the default when
             output is not to a terminal.

     -A      List all entries except for . and ...  Always set for the super-user.

     -a      Include directory entries whose names begin with a dot (.).

:
```

![](img/vsc_terminal.png)

## SSHing into StorrsHPC
Before we learn about about how to navigate the file system and move things around, let's
to log into Storrs HPC. We can do that from the terminal by using a secure shell (SSH), which is a
network protocol used to connect to remote computers.  To log into Storrs HPC, type on the terminal the following command:
```Bash
ssh YourNetID@login.storrs.hpc.uconn.edu
```
where YourNetID is your UConn username. You will be prompted for your password. Once you log in, you should see a welcoming message
with instructions. Anytime

*To access StorrsHPC from a computer connected to a network off campus you will need the [UConn VPN](https://confluence.uconn.edu/ikb/remote-access/virtual-private-network-vpn/accessing-the-uconn-network-through-a-vpn-client).*

## Key points

  - This course aims to empower you to use modern computer software to solve research problems in Marine Sciences.
  - The terminal or Unix shell is an application for the user to interact with the computer.
  - Secure Shell (SSH) is a network protocol used to access remote computers.


## Further reading

  - [Storrs HPC wiki](https://wiki.hpc.uconn.edu/index.php/HPC_Getting_Started).
  - [Bash cheatsheet](https://github.com/LeCoupa/awesome-cheatsheets/blob/master/languages/bash.sh)
