## Jupyter Books

Logging experience August 4, 2020. 

- [Jupyter-Earth case study](https://github.com/pangeo-data/jupyter-earth#build-the-documentation) 
- [beta.jupyterbook.org](https://beta.jupyterbook.org/start/overview.html)
- install with `pip install -U jupyter-book` in my Pangeo JupyterLab instance: check!
  - Returning to the environment: Re-install seems to check that everything is ok...
  - However running `jupyter-book create tmpbook` did not work so possible bug
  
  
> Possible bug: Does installing jupyter-book and then stopping the server and then returning create a "Wha???" situation? 
> Reproduce this by running `jupyter-book create tmpbook` after the install; and then shut down the server, come back later, 
> and try `jupyter-book create tmpbook1` to see what happens. 
  
  
Now we need a folder containing the markdown / notebook files; plus table of contents and (optional) configuration YAML files. 
I'm going to do this as a repository in `pangeo-data` following the jupyter-earth model; so jupyter-ocean. Choosing not to 
clone jupyter-earth; rather starting from scratch (README + MIT license). 

In my Pangeo pod

```
git clone https://github.com/pangeo-data/jupyter-ocean
```

I proceeded to edit this folder

- Added notebook `chlorophyll.ipynb`
  - Edits --> small size --> refers to some local files (mp3 etc)
  - oriented towards middle school
  - The Python code here attempts to install the ocean color map library cmocean; and some other tricky stuff
- synch back to GitHub via `git push`
- Back on GitHub in the jupyter-ocean repo:
  - Created a `_toc.yml` file with a single entry for the chlorophyll notebook.


