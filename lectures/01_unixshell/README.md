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
introduce other essential commands as they become necessary to perform our assignments.  


### Linux and MacOS users
Both Linux and MacOS are Unix-based operating systems, and the Unix shell is a
native application. The most common Unix shell application is called `Terminal`.

### Windows users
For Windows users I recommend the Unix terminal that come with [Visual Studio Code](https://code.visualstudio.com),
a Microsoft text edit that has become the go-to tool for software developers. VSCode
also works on Linux and MacOS.

## Basic commands

### Navigating the file system

To navigate the file system, we use two commands: `ls' (list) and `cd' (change directory).
```Bash
ls
```

### Moving files

To move files around, we use two commands: `cp' (copy) and `mv' (move).




![](img/vsc_terminal.png)

## Logging into StorrsHPC
To log into StorrsHPC, we use the secure shell (ssh) command:
```Bash
ssh YourNetID@login.storrs.hpc.uconn.edu
```
where YourNetID is your UConn username. You will be prompted for your password.

*To access StorrsHPC from a computer connected to a network off campus you will need the [UConn VPN](https://confluence.uconn.edu/ikb/remote-access/virtual-private-network-vpn/accessing-the-uconn-network-through-a-vpn-client).*



## Key points

  - This course aims to empower you to use modern computer software to solve research problems in Marine Sciences.
  - The terminal or Unix shell is an application for the user to interact with the computer.
  - Secure Shell (SSH) is a network protocol used to access remote computers.

  ---
  **Terminal** (Unix shell)

  It works with almost all markdown flavours (the below blank line matters).

  ---  
