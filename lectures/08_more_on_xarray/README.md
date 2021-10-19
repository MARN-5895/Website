# Lesson 8: More on xarray and remakrs on CF-compliant netCDF files
Today we will continue to learn about xarray: a python library for dealing with multidimensional label arrays. Let's fire up a blank jupyter notebook and start hacking!

### CF-compliant netCDF files
The climate science community has come up with conventions for climate and forecast (CF) metadata for Network Common Data Form (netCDF) files. As we mentioned before, netCDF is a platform-independent binary format for scientific data with metadata (including a file heading and attributes for each variable). Xarray was developed to work with netCDF data.

According to the CF convention authors, "conventions define metadata that provide a definitive description of what the data in each variable represents, and of the spatial and temporal properties of the data. This enables users of data from different sources to decide which quantities are comparable, and facilitates building applications with powerful extraction, regridding, and display capabilities." In short, CF conventions standardize key variable names, units and description to facilitate intercomparisons data products. You can find more about CF conventions and conformance [here](https://cfconventions.org/conventions.html). You can find more about netCDF [here](https://www.unidata.ucar.edu/software/netcdf/).

