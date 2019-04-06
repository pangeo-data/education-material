# core

Ideas and notes on learning Python for geoscience... what is essential? 

## Links

* Damien Irving's [Python Atmosphere and Ocean Sciences Lesson](https://carpentrieslab.github.io/python-aos-lesson/)
(Software Carpentry, raster emphasis)]
  * [My notes on running through Damien's lessons](https://github.com/pangeo-data/education-material/tree/master/pedagogy)
* Description of the [Python Climate/Weather Stack](https://drclimate.wordpress.com/2016/10/04/the-weatherclimate-python-stack/)

## notes on going through [Damien's AOS Python SC lesson](https://carpentrieslab.github.io/python-aos-lesson/)

### Lesson 1 
- *Before You Start* is a key thing; a few things one does without any context that makes sense shortly...
  - e.g. Create an environment via Anaconda username is great; helped much in advance by "create an Anaconda username"
  - `bash` is assumed (?) so the advance step of installing `bash` and reviewing via pointers basic Linux could help 
- We might agree upon a mental model of the compute environment 
- kudos for mention `Miniconda`; I would add a note on when Miniconda trades off w conda
- explanation of `channels` and `conda-forge` is a little light; but gotta say awesome that it is there
- is `conda list > environment.yml` a legit thing? Mention here? 
- also option here to describe the Python command line, `.py` scripts and Jupyter cells as 3 alternatives
  - introduce kernels as execution threads with their own state variables
- big conda install needs a remark on <time> = several to many minutes
  - plus I don't want to do this twice, the second time being the `pyaos-environment` version. Just once please.
    - I get the idea of the install above when I do `conda install xarray`



## Frustrations (unsorted grumbling) unrelated to the above

### Theme: A learning model that *works* without being *onerous* 

- Seeing 'this is how you do X in Python' is but one step in making the thing stick 
  - Note that this implies an exponential explosion of exposition... 
    - gotta abbreviate that X^3 yah? We need an economy of presentation material
      - Damien's AOS Lesson 1 is a good example of such economy
    - We do have the option of presenting a *learning model*
      - Example: Learn something new by building in:
        - Motivation: Here is an end result (now let's see the Pythonic route to that end)
        - Procedure: Here is a piece of code that does such and such
        - Context: Here is a larger context where this plays a key role
        - Debug: It can fail; so here is at least one way to unpack that fail and fix the problem
        - Constructive: If you had to invent this (say it did not exist) how would you start thinking about it?

### Theme: How do I know things are ok or haywire (and then how to debug)? (non-pink-ink scenarios)

- Anecdotal: I download :( raw 0.1deg MODIS Chlorophyll-A data from **NEO** and with some effort
xtract a small spatial subset; and with further gymnastics consolidate `n` source images into a single 
Dataset with a `time` dimension... but then subsequent operations on the Dataset are ludicrously slow. 
- 'This can't be right...' so I save this small Dataset to a file using `.to_netcdf()` and then open that file; 
now the Dataset responds instantly as it should. Unfortunately I *stumbled upon* this solution. 
  - How about `.load()`? 
- ***The insidious problem: If I do not *know* my data manipulation code should run fast I am in danger of 
accepting 'annoyingly slow' as normal and I curtail my exploration of the data based on my patience.*** 


```
# pre-processor for adding a sortable 'time' Data variable dredged up from the Dataset attributes
def pp(ds):
    # The author of this code has not deigned to explain why he added 15 days to each timestamp... but I expect
    #   that the data are published monthly so this places the time value at mid-month.
    ds['time'] = xr.Variable('time', [pd.Timestamp(ds.attrs['time_coverage_start']) + pd.Timedelta(15, unit='d')])
    return ds

# This aggregates five files into a single Dataset: One per month MODIS Chlorophyll-A raw data from NEO
cb = xr.open_mfdataset('modis_chlora_2017_*.nc', preprocess = pp, concat_dim='time').chlor_a.to_dataset() 

# Create a bounding-box Dataset, 21 x 21 in latitude x longitude
latselect = np.arange(44.52897-1., 44.52897+1.00001, 0.10)
lonselect = np.arange(-125.38966-1., -125.38966+1.00001, 0.10)
local = cb.sel(lat = latselect, lon = lonselect, method = 'nearest')

# 441 time-series plots on one chart
# this requires Age-Of-The-Universe time to not complete and is certainly bad form
p,a=plt.subplots(figsize=(13,9))
for i in range(21):
    for j in range(21):
        a.plot(local.time.values, local.chlor_a.isel(lat=i,lon=j).values, 'o-')

# write the 'local' Dataset to a new file (which upon reloading will be very fast)
# This reduces 250MB of data across five files to 30kb in one file, forsooth
#   Experiment to try: Issue local.load() and see if it has the same speed-up effect
local.to_netcdf('local.nc')    
```

### Theme: 'Best practices' is a nice phrase... but maybe tell me how do I avoid 'worst practices'

- Some older code that I wrote created a variable called `sum` so that when I subsequently discovered 
there is a Python function `sum()` and I tried to use it I got an error message `integer is not callable`. 
- There is some sort of namespace clobber term for this which I don't know; but that is how a clueless
programming step obscured a useful function; and sadly many minutes were burned figuring this out.
- Suppose one is a long-time C / procedural programmer like me (Rob (life spent writing nested for-loops)).
See above. Force of habit impedes me from learning abstractions that do away with for-loops. 
- On behalf of all the impatient people who don't bother to learn Python from the 
ground up (perhaps coming from another programming language) there is a need for 
a big ***Stop Sign*** that makes the case for developing an accurate model-plus-vocabulary for talking
about Python. 




