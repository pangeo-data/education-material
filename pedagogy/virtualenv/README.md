# Python virtual evironments

* [GitHub cookbook recipe](https://uoa-eresearch.github.io/eresearch-cookbook/recipe/2014/11/26/python-virtual-env/)
* [cloudmaven.org resource](https://cloudmaven.github.io/documentation/rc_jupyterhub.html)

```
conda create -n mycustomenvironment anaconda
source activate mycustomenvironment
```

This is like creating a swimming pool (first command) and then jumping into it (second command). 

What I hope to cover here is how a virtual environment works, the basic mechanics of jumping in and out; 
and relevance to building customization that works in a binder instance.

Questions to answer are: 

- What do we find once we jump in the pool? Looking ahead to binder: Is it minimalist?
- How do I jump back out again?
- From within: Can we test an empty world transfer to binder? How? Does it work?
- Once that is managed let's try and install yodapy and run a couple lines of it; same test: binder



