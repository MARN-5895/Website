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

## Step 1: Install [miniconda](https://docs.conda.io/en/latest/miniconda.html) in your home directory

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

The flag `-O` above is changing the name of the downloaded file (the output) to miniconda.sh. The download may take several seconds to complete.

## Step 2: Run Miniconda3

Now you can run the script script `miniconda.sh` to install the Anaconda package manager. The trick is to specify an installation directory within your home directory to avoid attempting to install `miniconda` system-wide (which only HPC IT folks have permission to do). To run the installation script type:

    bash miniconda.sh -b -p /home/NetID/miniconda/

This installation may take a few minutes to complete, because `miniconda.sh` will download and install all the basic Anaconda software (just like executing a .exe or .dmg file on you computer).

You should now check that the path to miniconda is in your terminal configuration file `.bashrc`,  which lives in your home directory. You can do that by printing the contents of `.bashrc` on the terminal:

    cat ~/.bashrc

where `~/` is a shortcut for `/home/NetID`. (If you are currently on your home directory, you don't need to add `~/`.) You should see an output whose last few lines look like these:

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
**If you don't see this, you should copy the code above and add it at the bottom of your `.bashrc`. You can do this in the terminal using the text editors `nano` or `vim`**. For example:

    nano .bashrc

will open `.bashrc` in the `nano` text editor. Remember to change NetID to your UConn username. In `nano`, to save changes and exit you should use `Crtl+O` and `Crtl+X`, respectively. In `vim`, you should do `esc` and then `:wq`.

Now that you have the miniconda path in your `.bashrc`, you need to ensure your terminal session is cognizant of the recent changes in the bash configuration file. You can do this by "sourcing" `.bashrc`:

     source .bashrc

We check that this worked using the shell command `which`:

    which conda

which should output the path where conda has been installed

    /home/NetID/miniconda/bin/conda

To check which version of conda you have installed, type

    conda --version

which should output

    conda 4.10.3

(the latest version).


## Step 3: Create a custom conda environment
You now have to install the python packages we will need. By default, miniconda comes with elementary
python packages, but it does not come with most of the packages we use for computational research. A good way to install these packages is to build a custom [conda environment](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-from-an-environment-yml-file). Working with environments helps you keep track of the versions and releases of packages you used for a specific project. Conda helps you toggle back and forth between different environments, thus allowing you to run different software versions that may be required for different projects.  Below is a `marn5895.yml` file created for this class:

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

You can copy this file from the course's shared space to your home directory:

    cp /shared/marn5895/marn5895.yml /home/NetID

If you are currently in your home directory (i.e., if `pwd` returns `/home/NetID`), you could
replace `/home/NetID` above with `.`, which is a short cut for the path of your current directory.

## Step 4: Create the conda environment

You should now be able to run the following command:

     conda env create --file marn5895.yml

This will download and install all the packages listed in `marn5805.yml` as well as their dependencies. It may take several minutes to complete this step.

## Step 5: Activate the environments

The environment you created needs to be activated before you can use the packages you installed. You will need to do this every time you log into Storrs HPC. To activate the `marn5895` environment, use the command `conda activate`:

     conda activate marn5895

Now you are in the `marn5895` conda environment as the prefix (marn5895) in your terminal suggests. To check that you have
`jupyterlab` and its dependencies installed in this environment, type

    conda list jupyterlab

which should output
```BASH
# Name                    Version                   Build  Channel
jupyterlab                3.1.9              pyhd8ed1ab_0    conda-forge
jupyterlab_pygments       0.1.2              pyh9f0ad1d_0    conda-forge
jupyterlab_server         2.7.2              pyhd8ed1ab_0    conda-forge
```
(To list all packages installed in the environment, simply do `conda list`.) In lecture 2, you will learn how to launch `jupyterlab`
on Storrs HPC and tunnel it to your local, meaning that `jupyterlab` will be running on Storrs HPC but you will be interacting with it on your local browser. This will give us a convenient working environment for this class.

You should also check that `IPython` (an enhanced interactive Python shell) was installed:

    conda list ipython

which should return 

```BASH
# packages in environment at /Users/crocha/anaconda3:
#
# Name                    Version                   Build  Channel
ipython                   7.16.1           py38h5ca1d4c_0  
ipython_genutils          0.2.0                    py38_0  
```

You can now open `IPython`:

    ipython

and fool around with it a bit. For example, you can do some algebra:

```PYTHON
a = 1
b = 2 
a+b
```
which obviously should return `3`.

You can also try the `print` function:

```PYTHON
print("\n\nHello world!\n\nI just completed my first MARN5895 in-class assignment, so I'm feeling good \U0001F60E.\n\nI \u2764\ufe0f  coding!\n")
```

To exit the `IPython` prompt, use `Crtl+d`.

## Extra: Adding packages to the environments (no action needed now)

Sometimes we will need to add packages to the environment after it has already been created using the above steps. For example, to install the R kernel packages, do:

    conda install -c r r-irkernel

If needed you can also update the environment from the environment file. This involves two steps:

    - Update the marn5895.yml file, adding new package names to it.
    - run `conda env update -f marn5895.yml --prune`

If you just want to update the packages that are already there and maybe new versions are available, then use `conda update --all`. We will come back to installing more packages and updating the conda environment in the future.

## Further resources

  - [Conda environments documentation](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#activating-an-environment)
  - [Software Carpentry conda lesson](https://carpentries-incubator.github.io/introduction-to-conda-for-data-scientists/setup/)
