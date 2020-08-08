## Jupyter Books

Logging experience August 4, 2020. 

- [Jupyter-Earth case study](https://github.com/pangeo-data/jupyter-earth#build-the-documentation) 
- [beta.jupyterbook.org](https://beta.jupyterbook.org/start/overview.html)
- install with `pip install -U jupyter-book` in my Pangeo JupyterLab instance: check!
  - Returning to the environment: Still installed: check!
  
Now we need a folder containing the markdown / notebook files; plus table of contents and (optional) configuration YAML files. 
I'm going to do this as a repository in `pangeo-data` following the jupyter-earth model; so jupyter-ocean. Choosing not to 
clone jupyter-earth; rather starting from scratch (README + MIT license). 

In my Pangeo pod

```
git clone https://github.com/pangeo-data/jupyter-ocean
```

I proceeded to edit this folder: Added notebook `chlorophyll.ipynb`. Edited it down to a reasonably small size; 
put in language oriented towards middle school; added some content files (mp3, mp4, jpg).


Interesting point: The Python code here attempts to install the ocean color map library cmocean; and so on. 
Dunno if this will work out.   

