# Assignment 1: Setting up conda and Jupyterlab on Storrs HPC


Most of our work in this class will take place on
[Jupyterlab](https://jupyterlab.readthedocs.io/en/stable/), an IDE than runs on
the browser. Jupyterlab was originally developed for Python, but now also
supports R and other languages. Conviniently, Jupyterlab supports Jupyter
notebooks, text editors, and a terminal. We will run jupyterlab on Storrs HPC
but open it on our local browsers, so that we can conviniently work remotely.

The easiest way to install Jupyterlab and Python packages used for
computational research is to use Anaconda's python distribution. Follow the steps below to
install a miniconda, create a working environment with basic packages, and
troubleshoot Python.

## Step 1: Install [miniconda](https://docs.conda.io/en/latest/miniconda.html) in user space.

Miniconda is a mini version of Anaconda that includes just conda and its dependencies. It is a very small download. If you want to use python 3 (recommended) you can call

    wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -O miniconda.sh

## Step 2: Run Miniconda3

Now you actually run miniconda to install the package manager. The trick is to specify the install directory within your home directory, rather in the default system-wide installation (which you won't have permissions to do). You then have to add this directory to your path. (Miniconda may do this automatically for you when running the bash script.)

    bash miniconda.sh -b -p $HOME/miniconda
    export PATH="$HOME/miniconda/bin:$PATH"

Make sure to check the path to miniconda is correct in the `.bashrc` file which should be in your home directory.

## Step 3: Create a base custom conda environment 
You now have to define what packages you actually want to install. A good way to do this is with a custom [conda environment file](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-from-an-environment-yml-file). Working with environments helps you keep track of the versions and releases of packages you used for a specific project. Conda helps you toggle back and forth between different environments, thus allowing you to run different software versions that may be required for different projects.  Below is an `environment.yml` that Cesar used for his undegraduate class MARN-3002: 

    name: marn3002
    dependencies:
     - numpy
     - scipy
     - pandas
     - xarray
     - netcdf4
     - dask
     - jupyterlab
     - matplotlib
     - cartopy
     - pip:
       - pytest

And here's another environment Cesar used to run [CODAS](https://currents.soest.hawaii.edu/docs/adcp_doc/), which doesn't work with the most recent matplotlib version:

    name: codas2020
    channels:
    - conda-forge
    dependencies:
    - mercurial
    - pip
    - pyflakes
    - numpy
    - flake8
    - python==3.7.9
    - matplotlib == 3.0.3
    - ipython

Create a similar files for your projects and save the as
`<environment_name>.yml`. You should choose a `name` that is descriptive of your project.

## Step 4: Create the conda environment

You should now be able to run the following command

     source .bashrc
     conda env create --file <environment_name>.yml

This will download and install all the packages and their dependencies.

## Step 5: Activate the environments

The environment you created needs to be activated before you can actually use it. To do this, you call

     conda activate marn3002

You should replace `marn3002` with whatever environment name you chose in your `environment.yml` file. This step needs to be repeated whenever you want to use the environment (i.e. every time you launch an interactive job or call python from within a batch job).

## Step 6: Adding packages to the environments

Sometimes we will need to add packages to the environment after it has already been created using the above steps. If possible, one can also update the environment from the environment file. This involves two steps:

    - Update the environment.yml file, adding new package names to it. 
    - run `conda env update -f environment.yml --prune` 

If you just want to update the packages that are already there and maybe new versions are available, then use `conda update --all`.



