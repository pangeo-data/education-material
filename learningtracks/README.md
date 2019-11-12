Hmmm... what does "A.R.D." stand for?


In all that ensues: The central idea of pangeo education is: Don't learn magic spells; rather: learn to debug.
This is to avoid the frustration and lost time when those magic spells inevitably don't work.


# Learning Tracks


- **Deployment Engineer**: You want to build and manage a Pangeo instance
- **Research Team Lead**: You want to lead your group in using a Pangeo instance for your research
- **Researcher**: You want to use a Pangeo instance for your research
- **Data Publisher**: You want to create an ***analysis-ready*** dataset


## First things first

Before diving into the pangeo-provided learning resources below: We want you to know what 
tools and skills are going to be essential to your role that *aren't* provided by pangeo. 
Why? Because other resources will teach you things like `pandas` and data visualization much
better than pangeo could. Furthermore pangeo will happily provide you with pointers to 
those things we consider essential; or to things that are specific to particular research
domains. 

* `pandas` and `scikit-learn` can both be learned from Jake VanDerplas' excellent book
* Creating and publishing a domain-specific Python package
* `yodapy` for a domain example
* and so on


## Deployment Engineer: You want to build and manage a Pangeo instance


So you are going to be a DevOps engineer for a running Pangeo instance...


* Zero2Pangeo on Kubernetes Part 1: Basics
* Zero2Pangeo on Kubernetes Part 2: Expansion options, considerations, pointers
* Resource management considerations including cost


## Research Team Lead: You want to lead your group in using a Pangeo instance for your research


So you and your research team members are going to be working on a Pangeo instance...


* binder for binder Advocates
* build a Docker env/spec for Pangeo; and run repo2binder locally; and ... what else here?
* how to write code and work Pangeistically for Pangeo Advocates


## Researcher: You want to use a Pangeo instance for your research

So you are interested in using Python to analyze and interpret data; and you are ok with 
doing so in a *pangeistic* manner. Awesome, welcome to the great game. You'll need good
familiarity with the following:

* the xarray data model
* distributed dask: Laziness, elasticity, `.load()`
* binder for binder Users
* how to write code and work Pangeistically for Pangeo Users


## Data Publisher: You want to create an ***analysis-ready*** dataset


* How to zarr, cog, parquet and bigquery
* Intake catalogs: Publication
