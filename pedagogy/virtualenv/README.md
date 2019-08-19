# Python virtual evironments

* [GitHub cookbook recipe](https://uoa-eresearch.github.io/eresearch-cookbook/recipe/2014/11/26/python-virtual-env/)
* [cloudmaven.org resource](https://cloudmaven.github.io/documentation/rc_jupyterhub.html)

Command for working with Python environments using the Anaconda package manager: 

```
conda-env create -n custom anaconda
conda activate custom
conda deactivate
conda-env list
conda-env update
conda-env export
conda-env remove
```

The first two commands are like creating a swimming pool (first command) and then jumping into it (second command).
From there we want to be able to get back out of the pool (`deactivate`) and list the available pools (`list`). 


The remaining three `conda-env` commands are self-explanatory.


What I hope to cover here is how a virtual environment works, the basic mechanics of jumping in and out; 
and relevance to building customization that works in a binder instance.

Questions to answer are: 

- Looking ahead to binder: Is an environment minimalist?
- From within an env: How to test an empty world transfer to binder? Have someone else check fast spin-up?
- Once that is managed let's try and install yodapy and run a couple lines of it; same test: binder



