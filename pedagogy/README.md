# pedagogy

## purpose

This folder and its sub-folders are the accumulation zone for initial pangeo-ed content. "Process" work is more 
for the `wg` working group folder parallel to this `pedagogy` folder.


## community estimation

AGU fall meeting attendance of (say) 25,000 attendees implies a global academic geoscience population of 
perhaps 300,000 individuals and a commensurate non-academic population (industry, non-profit, military, 
governmental). Let's say a million people total. Precisely three of these people know how to use the Python 
geoscience stack effectively: Joe Hamman, Ryan Abernathy and a middle-school kid living in Boise Idaho. 
This leaves a potential learners pool of 999,997 people. We have a lot of work before us.


### What is the Python geoscience stack? 


Much like **pangeo** the Python geoscience stack is code plus mindset: 
'Learn Python so you can learn `numpy`. Learn `numpy` to then learn `pandas`. Learn `widgets` for interactivity, 
learn `utm` to use localized Cartesian coordinates, add in `ipyleaflet` for creating interactive maps, and you 
will need `matplotlib` of course; and some other packages I can't recall at the moment. Now you are prepared to 
learn `xarray` and `dask`... and now finally you are ready to use `pangeo` to analyze 12 Exabytes of 
MODIS and Landsat data. (Oh and sorry you also need to learn `bash` and `git` and `vim` and `Jupyter notebooks`.)


Clearly nonsense... but this does give a sense of building data science skill (using Python) as an 
involved process. What about attempting to circumvent all that? For example a certain scientist decided 
to learn `xarray` by simply writing a research paper in a Jupyter notebook. His idea was to focus on the
research and pick up the package details in passing. He began with a NetCDF-CF file:

```
d=xr.open_dataset('./data.nc')
d
```

He was pleased to find a torrent of text flooding across his screen:  Apparently simply naming the object caused it 
to describe itself. It was then that his troubles began. He could not print out a few data values. He could not 
generate plots... and even when he figured that out some of the data seemed to be -9999.0 so the plots were 
meaningless. Other segments of the data had value `NaN` and he spent several days 
trying to `drop` the `NaN` values which produced copious arcane error messages... but still the NaNs stubbornly
persisted. The senior scientist was torn: Should he dissolve in tears? Become a vindictive super-villain? Retire? 


Somewhere in here is an optimal learning path for us to derive. Some ideas:


- Read up on successful teaching and learning strategies; and copy success
- Include material that already exists and works, my favorite example being 
[Jake's handbook](https://jakevdp.github.io/PythonDataScienceHandbook/)
- Organize the PGS landscape from high-level view down to modular
- Create content where it is needed that pre-addresses gaps and misconceptions
  - Bad pre-existing knowledge bias can hinder learning
- Create domain-specific content together with an emissary program (Hacks, curriculum, classes at conferences, ...)
  - As possible: teach teachers
- Consider learner goals and include teaching elements from the outset that lead in those directions
  - For example "***Every*** PGS learner should start building a Python package from Day 1."
- Define and evaluate success metrics; particularly via working with the target audience
  


