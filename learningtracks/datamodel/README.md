# Introduction

Our *objective* is to optimize scientist skill. We present here a 
picture of data organization in the geospatial research ecosystem. This picture depends on a set
of interrelated *data models* which lead to data *access methods*.  


Pangeo's take on data models begins here.


UNIDATA has both a [common data model](https://www.unidata.ucar.edu/software/netcdf-java/v4.6/CDM/index.html) 
and a closely-related [NetCDF data model](https://www.unidata.ucar.edu/software/netcdf/docs/netcdf_data_model.html). 
We focus here on the latter, where [`NetCDF`](https://www.unidata.ucar.edu/software/netcdf/docs/index.html)
refers concretely to a data file format.


## fast-track bootstrap plan

An immersive sequence, much more in-depth:

* Learn Python
* Read the first three chapters of 
[Jake's book](http://xarray.pydata.org/en/stable/why-xarray.html)
(chapters 4 and 5 are great as well)
* Read the xarray online documentation
* Read the NetCDF online documentation
* Start up a binder notebook from [here] (link needed). 


## seagrinch remarks 


CDM: More a philosophy that communities should establish and use a CDM appropriate to their needs; established standards. 
In Oceanography, the 
[NODC NetCDF templates](https://www.nodc.noaa.gov/data/formats/netcdf/v1.0/#templatesexamples)
are a good place to start. Put your data in this format and it can easily be 
integrated into commonly used tools like Panoply and ERDDAP.


There’s really two parts to this… getting your data in the right format (e.g. timeseries, profiles, 4D grids) 
and including appropriate, required and standardized metadata, e.g. 
[CF Conventions](http://cfconventions.org/).


As for dimensions and data-types (aka objects in Python), I think I would try to distinguish between the two…


Coming from a Matlab world, things were a bit easier. First there are dimensions: Scaler (single value), 
Vector (columns of values) and Arrays (2D, 3D… ND). Then there are data types: e.g. integers, floats, 
strings (and many more annoying ones, like char and datetime). Structured arrays are great too; and 
very python-dictionary like.


Now in the Python world we have objects galore, and it’s often a challenge to mentally switch between them (lists and 
dictionaries being a good example).


In my training sessions, I’ve generally glossed over most of this, and basically stuck to trying to explain the 
differences and advantages between Pandas DataFrames (basically Excel tables - great for lots of individual measurements 
with 1…n variables/columns) and Xarray DataSets (which are great for multi-dimensional datasets, which of course is 
our bread-and-butter in geoscience).


In many cases, DataFrames and DataSets are interchangeable. The OOI dataset is a good example, where most instruments 
provide simple timeseries with multiple variables. So, which type you use really depends on the additional features 
of the library you wish to use (well, that and performance). But if you had a more complicated dataset, like a 
profiler dataset that had the dimensions Time and Depth, or optical data with a wavelength dimension, then xarray 
becomes essential.


### Rob has a follow-up question


I have been working with OOI profiler fluorometer data where `obs` is a default `dimension` 
that can quickly be swapped for `time`: `ds = ds.swap_dims({'obs':'time'})`. This makes sense to me since
time is a monotonic coordinate.  `int_ctd_pressure` is a second `coordinate` equivalent to profiler depth, 
conceptually a dimension of the data. Under what circumstances should this be added as another `dimension`?


## The data zoo

This section presents a "zoo" of data types, formats, and Pythonic access methods. I'm making very
little initial effort to organize it, kicking that task down the street.


### Linkage

* [UNIDATA Common Data Model](https://www.unidata.ucar.edu/software/netcdf-java/v4.6/CDM/index.html)
* [NetCDF documentation](https://www.unidata.ucar.edu/software/netcdf/docs/index.html)
* [NetCDF data model](https://www.unidata.ucar.edu/software/netcdf/docs/netcdf_data_model.html)
* [xarray](http://xarray.pydata.org/en/stable/why-xarray.html)
* [xarray data structures](http://xarray.pydata.org/en/stable/data-structures.html)


### NetCDF

#### Layers (conceptual, building up)

1. data access / syntactic layer: Data reading and writing.
2. coordinate system layer: Abstract but includes specialized georeferencing coordinate systems
3. scientific feature type layer: specific types of data such as grids, radial, and point data


### Python

#### Basic types

* native: string, integer, float, ...
* aggregate/enumerable: tuple, list, dictionary, what `range()` returns... (mutability)
* ndarray from numpy

#### pandas Dataframes

#### from pandas to geopandas

#### from geopandas to xarray
http://xarray.pydata.org/en/stable/data-structures.html

#### from xarray to dask

#### from dask to 
