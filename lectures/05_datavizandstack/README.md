# Lesson 5: The Python scientific stack and data visualization


## A whirlwind tour of the Python Scientific stack

![](img/SciPythonStack.png)


The Python scientific stack (aka python scientific ecosystem) is a set of libraries, modules and toolboxes widely used 
in scientific applications. See the image above, adapted from Jake Vanderplas, depicting the stack. 

All these tools build on Python and some of them also wrap code from compiled languages such as C and 
Fortran. The core scientific python modules include packages such as IPython and Jupyter Lab for interactive computing, numpy for 
fast array operations, Cython for converting/computing in C a code that's writting mostly in Python, numba for compiling parts of a Python code, and 
Dask for parallel computing. Building on those tools, there are many libraries scientists use on a daily basis, such as matplotlib for data visualization, 
scipy for efficient numerical operations, pandas for manipulating tabular data, and xarray for multidimensional arrays. On top of those tools are the more 
specialized packages such as scikit-learn for machine learning and sympy for simbolic mathematics. More specialized packages, which as specific to a field or subdiscipline, 
builds on all the inner layers.

We will learn some of those tools in the coming several weeks. For now, open a blank notebook and name it `05_sciencestack.ipynb`. Cesar will work through a quick introduction to numpy and scipy.

## Introduction to data visualization in Python
Let's now pivot to matplotlib. To use our time efficiently, let's work on the notebook for assignment 4 [`04_saildronedata.ipynb`](https://github.com/MARN-5895/Assignment-04/blob/main/04_saildronedata.ipynb). Please, open the notebook on your branch inside `~/MARN5895/Assignments/04/`.

### Extra resources

Here's an  [article](https://tos.org/oceanography/assets/docs/29-3_thyng.pdf) led by [Kristen Thyng](https://github.com/kthyng) about `cmocean` and colormaps in general. And here are a few plotting modules that you may want to check out:

1. [proplot](https://proplot.readthedocs.io/en/latest/) for publication quality graphics.
2. [seaborn](https://seaborn.pydata.org) and [altair](https://altair-viz.github.io/getting_started/overview.html) for statistical plotting.
3. [bokeh](https://bokeh.org) and [holoviews](https://holoviews.org) for interactive figures.
