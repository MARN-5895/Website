# Assignment 1: Setting up conda and Jupyterlab on Storrs HPC


Most of our work in this class will take place on
[jupyterlab](https://jupyterlab.readthedocs.io/en/stable/), an IDE that runs on
the browser. Jupyterlab was originally developed for Python, but now also
supports R and other languages. Conviniently, jupyterlab runs the Jupyter
notebook and has a text editor and a Unix terminal. We will run jupyterlab on Storrs HPC
but open it on our local browser, so that we can easily work remotely.

Using the [Anaconda](https://www.anaconda.com) packet manager is the easiest way to install jupyterlab and other Python packages used for computational research. **Please, complete the 5 steps below to
install miniconda, create a working environment with basic packages, and
check that your installation was successful.**

## Step 1: Install [miniconda](https://docs.conda.io/en/latest/miniconda.html) in user space.

Miniconda is a mini version of Anaconda that includes just conda (the package manager) and some elementary Python packages. We will download an
installation script and run it on Storrs HPC. First, log into Storrs HPC:

    ssh NetID@login.storrs.hpc.uconn.edu

where NetID is your UConn username. Now you landed in you home directory on an Storrs HPC access node. To check that, you can type the command `pwd` (print current directory), which should return:

    /home/NetID/

You should now run the bash script `launch_bash_slurm_marn5895.sh` to move into a work node dedicated to this course:

    bash launch_bash_slurm_marn5895.sh

We now will download the miniconda Linux installation script, available from the company that developed
and distributes the Anaconda package. (Remember that Storrs HPC uses a Linux Operating System.) The script is available online at [https://repo.continuum.io/miniconda/](https://repo.continuum.io/miniconda/). To download a file
directly from an URL, we use the command `wget` (Web get):

    wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -O miniconda.sh

The flag `-O` above is changing the name of the downloaded file (the output) to miniconda.sh.

## Step 2: Run Miniconda3

Now you can run the script script `miniconda.sh` to install conda, the Anaconda package manager. The trick is to specify a installation directory within your home directory, rather than the default system-wide installation (which you won't have permissions to do). You then have to add this directory to your path. (Miniconda may do this automatically for you when running the bash script.) To run the installation script type:

    bash miniconda.sh -b -p /home/NetID/miniconda/

This installation may take a few minutes to complete, because `miniconda.sh` will download and install all the basic Anaconda software (just like executing a .exe ).

Now you can add the directory to you path:

    export PATH="/home/NetID/miniconda/bin:$PATH"

Adding something to you path ensures that the terminal shell will recognize where the software (in this case the the Anaconda package manager) is installed, so when you type Anaconda commands, the terminal will recognize and execute them.

Make sure to check the path to miniconda is correct in the `.bashrc` file which should be in your home directory. You can do that by printing the contents of `.bashrc` on the terminal:

    cat ~/.bashrc

where `~/` is a shortcut for `/home/NetID`. The should see an output whose last few lines look like these:

```Bash
# >>> conda initialize >>>
# !! Contents within this block are managed by 'conda init' !!
__conda_setup="$('/home/NetID/miniconda/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
if [ $? -eq 0 ]; then
    eval "$__conda_setup"
else
    if [ -f "/home/NetID/miniconda/etc/profile.d/conda.sh" ]; then
        . "/home/NetID/miniconda/etc/profile.d/conda.sh"
    else
        export PATH="/home/NetID/miniconda/bin:$PATH"
    fi
fi
unset __conda_setup
# <<< conda initialize <<<
```

We can also check that `conda` has been installed using the shell command `which`:

    which conda

which should output the path where conda has been installed

    /home/NetID/miniconda/bin/conda

To check which version of conda you have installed, type

    conda --version

which should output

    conda 4.10.3

(the latest version).


## Step 3: Create a base custom conda environment
You now have to the python packages we will need. By default, anaconda comes with basic
python packages, but it does not come with some of the packages we use for computational research. A good way to install these packages is to build a custom [conda environment file](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-from-an-environment-yml-file). Working with environments helps you keep track of the versions and releases of packages you used for a specific project. Conda helps you toggle back and forth between different environments, thus allowing you to run different software versions that may be required for different projects.  Below is a `marn5895.yml` file that Cesar created for this class:

```BASH
name: marn5895
channels:
 - conda-forge
dependencies:
 - pip
 - numpy
 - scipy
 - pandas
 - xarray
 - netcdf4
 - dask
 - jupyterlab
 - matplotlib
 - cartopy
 - cmocean
 - proplot
 - pip:
   - pytest
```

You can copy this file from the MARN5895 shared space to you home directory:

    cp /shared/marn5895/marn5895.yml /home/NetID

If you are currently in your home directory (i.e., if `pwd` return `/home/NetID`), you could
replace `/home/NetID` above with `.`, which is a short cut for the path of your current directory.

## Step 4: Create the conda environment

You should now be able to run the following command

     source .bashrc
     conda env create --file marn5895.yml

This will download and install all the packages listed `marn5805.yml` as well as their dependencies. It may take several minutes to complete this step.

## Step 5: Activate the environments

The environment you created needs to be activated before you can actually use it. You will need to do this every time
you log into Storrs HPC. To activate the `marn5895` environment, use the command `conda activate`:

     conda activate marn5895

Now you are in the `marn5895` conda environment as the prefix (marn5895) in your terminal suggests. To check that you have
`jupyterlab` and its dependencies you have installed in this environment, type

    conda list jupyterlab

which should output
```BASH
# Name                    Version                   Build  Channel
jupyterlab                3.1.9              pyhd8ed1ab_0    conda-forge
jupyterlab_pygments       0.1.2              pyh9f0ad1d_0    conda-forge
jupyterlab_server         2.7.2              pyhd8ed1ab_0    conda-forge
```
(To list all packages installed in the environment, simply do `conda list`.) In lecture 2, you will learn how to launch `jupyterlab`
on Storrs HPC and tunnel it to your local. This will give us a convenient working environment for this class.


## Extra: Adding packages to the environments (no action needed now)

Sometimes we will need to add packages to the environment after it has already been created using the above steps. If possible, you can also update the environment from the environment file. This involves two steps:

    - Update the marn5895.yml file, adding new package names to it.
    - run `conda env update -f marn5895.yml --prune`

If you just want to update the packages that are already there and maybe new versions are available, then use `conda update --all`. We will come back to installing more packages and updating the environment in the future.

## Further resources

  - [Conda environments documentation](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#activating-an-environment)
  - [Software Carpentry conda lesson](https://carpentries-incubator.github.io/introduction-to-conda-for-data-scientists/setup/)
