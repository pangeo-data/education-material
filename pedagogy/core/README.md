# core

Ideas and notes on learning Python for geoscience... what is essential? 

## Links

* Damien Irving's [Python Atmosphere and Ocean Sciences Lesson](https://carpentrieslab.github.io/python-aos-lesson/)
(Software Carpentry, raster emphasis)]
* [My notes on running through Damien's lessons](http://github.com/pangeo-data/education-material/pedagogy/README.md)
* Description of the [Python Climate/Weather Stack](https://drclimate.wordpress.com/2016/10/04/the-weatherclimate-python-stack/)


## Frustrations (unsorted grumbling)

### Theme: How do I know what's expected versus what is aberrant? Then how do I debug?
- Being polemical again: Seeing 'this is how you do X in Python' is step one (only) of about five steps
needed to make it useful. The additional steps include 'Suppose this is not working; how do we approach
debugging it?'
- Anecdotal: I download :( raw 0.1deg MODIS Chlorophyll-A data from **NEO** and go to considerable 
length to extract a small spatial subset; with further gymnastics to consolidate `n` source images into a single 
Dataset with a `time` dimension... so far so good... and then subsequent operations on the Dataset are ludicrously
slow. 
- I save this small Dataset to a file using `.to_netcdf()` and then open that file; now the Dataset responds 
instantly as it should.
- I had an earlier version of this experience where `.load()` was a solution.
- The insidious problem is that if I do not *know* that it should respond fast I am in danger of accepting 'it is slow'
as the norm; so I curtail my exploration of the data based on my patience. 


```
def pp(ds):
    ds['time'] = xr.Variable('time', [pd.Timestamp(ds.attrs['time_coverage_start']) + pd.Timedelta(15, unit='d')])
    return ds

# five files: One per month MODIS Chlorophyll-A raw data from NEO
cb=xr.open_mfdataset('modis_chlora_2017_*.nc', preprocess = pp, concat_dim='time').chlor_a.to_dataset() 
latselect = np.arange(44.52897-1., 44.52897+1.00001, 0.10)
lonselect = np.arange(-125.38966-1., -125.38966+1.00001, 0.10)
local = cb.sel(lat = latselect, lon = lonselect, method = 'nearest')

# this requires Age-Of-The-Universe time to never complete and is certainly bad form on top of it
p,a=plt.subplots(figsize=(13,9))
for i in range(21):
    for j in range(21):
        a.plot(local.time.values, local.chlor_a.isel(lat=i,lon=j).values, 'o-')

local.to_netcdf('local.nc')    # reducing 250MB in five files to 30kb in one file, forsooth

```

### Theme: 'Best practices' is a nice phrase... but maybe tell me how do I avoid 'worst practices'

- Some older code that I wrote created a variable called `sum` so that when I subsequently discovered 
there is a Python function `sum()` and I tried to use it I got an error message `integer is not callable`. 
- There is some sort of namespace clobber term for this which I don't know; but that is how a clueless
programming step obscured a useful function; and the real crime is how many minutes it took me to figure
this out. 
- That is, on behalf of all the impatient people out there who don't bother to learn Python from the 
ground up (and I think a lot of us are coming from another programming language) there is a need for 
a big ***Stop Sign*** that makes the case for developing an accurate model-plus-vocabulary for talking
about Python. 




