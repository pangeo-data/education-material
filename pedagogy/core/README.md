# core

Additional ideas and notes on learning Python for geoscience. 

## Stuff that I find particularly frustrating (unsorted grumbling)

- I download :( raw 0.1deg MODIS Chlorophyll-A data from **NEO** and go to considerable 
length to extract a small spatial subset; with further gymnastics to consolidate `n` source images into a single 
Dataset with a `time` dimension... and then it has the gall to be ludicrously slow. ***The theme here is how 
do I know what's expected versus what is aberrant? And then how do I debug??*** For example: I save the Dataset 
to a file, read it back in and it responds quickly as it should. The insidious problem is that if I do not 
*know* that it should be quick then I start curtailing my exploration of the data based on my patience. And
along related lines: How do I avoid bad patterns, 'worst practices'?


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

# Notes on Damien's [Python AOS Alpha](https://carpentrieslab.github.io/python-aos-lesson/)

## Links

* Damien Irving's [Python Atmosphere and Ocean Sciences Lesson](https://carpentrieslab.github.io/python-aos-lesson/)
(Software Carpentry, raster emphasis)]
* Description of the [Python Climate/Weather Stack](https://drclimate.wordpress.com/2016/10/04/the-weatherclimate-python-stack/)
