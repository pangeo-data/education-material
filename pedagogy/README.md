This README file is set in stone and none of its content is negotiable for all time. 

# pedagogy

## notes on [Damien's AOS Python SC lesson](https://carpentrieslab.github.io/python-aos-lesson/)

### Lesson 1 
- Creating an environment by referring to Anaconda username is great; but suggest pre-load with "you will need an Anaconda username"
- Many of these comments have to do with having a mental model of the compute environment
- `bash` is assumed; installing `bash` plus a Linux ramp would go into `core` as 'this is necessary, here are the refs'
- kudos for mention `Miniconda`; I would add a note on when Miniconda tradeoffs w conda
- explanation of `channels` and `conda-forge` is a little light; but gotta say awesome that it is there
- is `conda list > environment.yml` a legit thing? Mention here? 
- also option here to describe the Python command line, `.py` scripts and Jupyter cells as alternatives
  - introduce kernels as execution threads with their own state variables
- big conda install needs a remark on <time> = several to many minutes
  - plus I don't want to do this twice, the second time being the `pyaos-environment` version. Just once please.
    - I get the idea of the install above when I do `conda install xarray`


## polemics

The 25,000 annual attendees at AGU (and similar geoscience conferences scaling down from there) imply a 
global academic geoscience community of some 300,000 persons (say) with a commensurate non-academic 
population. Of these precisely three know how to use the Python geoscience stack effectively: Joe Hamman, 
Ryan Abernathy, and some middle-school kid living in Cleveland Heights. This leaves a potential learners pool
of 599,997 people all of whom have unlimited spare time and enthusiasm for learning from the materials
we produce here. And they are collectively responsible for saving planet earth for future human habitation.
This page covers all the basics. 


### What is the Python geoscience stack? 


Much like **pangeo** the **PGS** is as much a philosophy as it is code. It states in effect 'If you learn
Python first then `numpy` will be easier to learn. If you learn `numpy` then `pandas` will be easier to 
learn. And so forth through `widgets` for interactivity, `utm` for localized Cartesian coordinates, 
`ipyleaflet` for creating interactive maps, `matplotlib` of course; and some other packages I can't think of at the moment. 
Then and only then will it become relatively *easy* for you to learn `xarray` and thence `dask`. Finally
once you have mastered dask you will be ready to use `pangeo` technology to analyze 12.4 Exabytes of 
MODIS and Landsat data. (Oh and we almost forgot you also need to learn the `bash` shell and `git`
and `vim` and `Jupyter notebooks` in parallel.)


Clearly this is nonsense. However a glimmer might be present as exemplified in this cautionary tale: 


A certain senior scientist decided one day to learn `xarray` by simply writing a research paper on a Jupyter 
notebook. He began with a NetCDF-CF file:

```
d=xr.open_dataset('./data.nc')
d
```

He was pleased to find a torrent of text flooding across his screen:  Apparently simply naming the object caused it 
to describe itself. It was then that his troubles began. He could not print out a few data values. He could not 
generate plots... although Stack Overflow did provide a magic spell for plots; but then some data was clearly -9999.0
and the resulting plots were un-watchable. Other segments of the data had value `NaN` so he spent several days 
trying to `drop` the `NaN` values which produced copious arcane error messages... but still the NaNs stubbornly
persisted. The senior scientist was torn: Should he dissolve in tears? Or should he become a vindictive super-villain? 


Somewhere in between these two extremes is an optimal learning path for us to derive. To begin with we have in our
toolbox the open tools that we use every day; so we are ahead of the game in this regard. We have **binder**, we
have **colab**, and so on. So ok yeah but then what? We are still a long ways from being effective. 


The only approach I'm aware of that has a chance of working includes at least the following factors:


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
  


