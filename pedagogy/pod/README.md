# pods

## Overview


This discussion concerns working in a Python environment embedded in a Linux operating system; presuming that
the source material (particularly Jupyter notebooks) is preserved as a repository ('repo') on GitHub.


When we land in a Jupyter notebook environment -- say **binder** or **colab** or a **JupyterHub** --
we ask 'Just where am I right now?' This document answers that question with practical implications. 
Let's begin with a little joke: "You are standing in a **pod** at the end of a road before a small brick building.
Around you is a forest.  A small stream flows out of the building and down a gully."

Ok *actually* a pod can be thought of as a computer with a built-in working environment. 
When we work at a computer we are 
accustomed to stopping at some point (say for lunch) and coming back later. The computer is still
there. However a pod is a construct *on* some computer; and so the question of its persistence is very
important. A pod may persist for days or weeks or indefinitely; or on the other hand a pod may evaporate in a 
matter of minutes or hours if you stop using it.  Even if it persists it might still stop from time to time
and need to be re-started. Pods that should persist must be reliably save-able and re-startable.


#### Get pod parameters using Python

Work in progress; need to add disk space bit... flag
Work in progress; need to add load data via shell script file after configuration is done... flag


We can use `psutil`, the Python system and process utility package, to get a read-out on the virtual machine
where the pod resides. For example: In a Jupyter notebook cell enter and run this Python code: 


```
def tell_system_status():
        # from https://www.programcreek.com/python/example/53878/psutil.disk_usage
        import psutil
        import platform
        import datetime

        os, name, version, _, _, _ = platform.uname()
        version = version.split('-')[0]
        cores = psutil.cpu_count()
        cpu_percent = psutil.cpu_percent()
        ram = psutil.virtual_memory().total >> 30
        memory_percent = psutil.virtual_memory()[2]
        disk_percent = psutil.disk_usage('/')[3]
        boot_time = datetime.datetime.fromtimestamp(psutil.boot_time())
        running_since = boot_time.strftime("%A %d. %B %Y")
        response = "I am currently running on %s version %s.  \n" % (os, version)
        response += "This system is named %s \n" % (name)
        response += "It has %s CPU cores.  \n" % (cores)
        response += "It has %s Gigabytes of RAM.  \n" % (ram)
        response += "Current disk_percent is %s percent.  \n" % disk_percent
        response += "Current CPU utilization is %s percent.  \n" % cpu_percent
        response += "Current memory utilization is %s percent. \n" % memory_percent
        response += "it has been running since %s. \n" % running_since
        return response 
    
print(tell_system_status())
```

The output will be something like this: 

```
I am currently running on Linux version 4.14.106.  
This system is named jupyter-kilroy
It has 8 CPU cores.  
It has 30 Gigabytes of RAM.  
Current disk_percent is 24.4 percent.  
Current CPU utilization is 0.0 percent.  
Current memory utilization is 11.8 percent. 
it has been running since Tuesday 23. April 2019.
```

This read-out is for the node (the virtual machine) that the pod lives on. It is not the pod resource/limits as 
given in the JupyterHub config. flag continue this thought below The effective resources available in the 
*pod* might be about half the above if the Hub spins up two user pods per virtual machine. 


#### ***Pro Tip: using `kubectl` and JHub config***

Pods are often created on clusters which are in turn orchestrated (turned on, turned off, 
configured, managed, ...) using a software framework called `kubernetes`. A kubernetes cluster has 
an interaction *command* which is `kubectl`. I like to pronounce this **koo - beck - tull** but that is no doubt 
incorrect. A shell command that begins with `kubectl` is an interaction with a kubernetes cluster of 
virtual machines that host pods. For example this command obtains a list of pod names from the bash prompt: 

```
kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}'
```
This one requests how much RAM is available:
```
kubectil top pod <pod-name-from-above>
```

flag this must be fixed: Another technical approach: Check the information available in the 
[JupyterHub config](https://github.com/pangeo-data/pangeo-cloud-federation/blob/eef3a575973f9789bcdb496b794e2334a88b4661/deployments/nasa/config/common.yaml#L59-L64)


## pangeo JupyterHub instance

## colab

## binder: On `mybinder.org` and on `pangeo.binder.io`

>  "A pangeo binder instance has a bare-bones jupyter environment by default that comes from repo2docker; nothing pangeo-related. 
An `environment.yml` or `requirements.txt` file will be noticed by repo2docker and used to install additional libraries, augmenting
the default environment. Once completed: An image of the pod is saved to skip (re-)building as long as the source material does
not change. That is: This image is tagged with the github commit time so (on launch) if the repo hasn’t changed the image won’t 
get rebuilt. As the image is based on the github tag (not on the user) multiple users can click the same link and each person 
gets a duplicate environment on their own pod." -Scott Henderson


I want my repository to be available in binder for two reasons! First it is a test of the portability of my 
repository as a working space. Second it allows me (when it works) to share my work with other people at a single
click with no authentication steps.


I would prefer to configure the binder pod using `environment.yml` rather than `requirements.txt`. The latter 
uses `pip` and the former uses the `conda` package manager.  Here is my example `environment.yml` configuration file. 


```
name: rca2binder-environment
dependencies:
  - python=3.7
  - rasterio
  - numpy
  - scipy
  - pandas
  - xarray
  - matplotlib
  - ipywidgets
  - pillow
  - traitlets
  ```
  
  

My source repo on GitHub is `rca2binder` and my GitHub 
organization is `cormorack`. I will use the `master` branch of this repo. I will use the `mybinder.org` binder
service. This is sufficient information to proceed. 


(If I try to use the `pangeo` binder instance the resulting pod will run Jupyter*Lab*
where widgets will not work. I want to make use of widgets so I will stay with the free `mybinder`
service. This in turn means that I'm not doing any dask at-scale computing for now. 


There are two paths to setting up a binder instance.


First path:


* Visit the wizard at the [binder.org website](https://mybinder.org)
  * A manual process leading to a binder session based on my repository 


Second path: 


* Go direct from a GitHub repo to a binder instance using a badge link
  * Install a *badge* directly into my repository `README.md` file
    * This auto-launches the repository in binder
  * Cause the binder session to pre-install software packages that my code needs
  * After configuration finishes: Load a modest-sized dataset into the pod
    * ...without having to store that data in the GitHub repository


Before going into further detail: A brief intermezzo on binder.


#### Conceptual basis

Using binder as a test environment encourages you (as a software developer) to work in an organized
manner; meaning in turn that your code will be comprehensible and debuggable and improveable. 


flag further ideas to touch upon here:
Indicate the binder registry spin up time.
Re-building the image when the hash changes; what changes the hash and what doesn't? 
How can I use binder as a sanity check on a package ensemble? 
When do I start resorting to environments? 
How does binder help streamline package installation? 
Is there always an implicit non-binder working environment? (Since binder is ephemeral...)
Who am I if I am creating a package?
How am I managing credentials?

Credentials: You may have a private authentication-protected binder instance. 
Without that you pass credentials from binder back to GitHub to update content; a 
practice that is discouraged. This implies you develop somewhere non-binder and
test deploy on binder.


#### Launch badge install in README.md at the root of the repository

To get the launch badge working: Edit the main `README.md` file at the root of your repository 
to include this line at the top of the file:

```
[![Binder](http://mybinder.org/badge.svg)](https://mybinder.org/v2/gh/cormorack/rca2binder/master)
```

This is binder version 2 (`v2`). The repo is hosted on GitHub (`gh`). 


The pangeo organization maintains its own binder instance called `binder.pangeo.io`. That would
be the URL used (twice) in the above in lieu of `mybinder.org`. 

On [GitHub](https://github.com) we find that the pange organization is `pangeo-data`. 
Therein the `pangeo-example-notebooks` repository is a good candidate for the pangeo binder instance; 
where again we choose the `master` branch. Consequently the `README.md` link reads:

```
[![Binder](http://binder.pangeo.io/badge.svg)](http://binder.pangeo.io/v2/gh/pangeo-data/pangeo-example-notebooks/master)
```

We *could* append `?urlpath=lab`. This is a key-value pair that translates
as "When all is said and done setting up this binder instance: Append `lab` to the binder URL." This has the effect
of establishing the working environment inside [**JupyterLab**](https://jupyterlab.readthedocs.io) which is the
very cool next-generation Jupyter notebook environment. This is an example of where the sidewalk ends: Going into
additional key-value pair features of this binder interface is out of scope. However we reiterate as noted above
that widgets are not compatible with JupyterLab at the moment; they may not work. 


#### Directing package installation in a binder launch

flag: Need to include the context of a terminal; and need to indicate the more complete `pip` procedure using a temp
environment (?) as noted at top of `ops/README`. pip.pypa.org maybe? search on pip_freeze probably works. 


There are (for our purposes) a couple of ways used (text files generated) to direct the installation of software 
packages for Python. Your choice of file name implicitly decides how the installation proceeds. Side note:
Other languages like **R** have similar mechanisms not described here. 


The first way to install packages as binder launches a session is to include a file recognized by the 
**conda** package manager. This file *must* be called `environment.yml` by convention. The second way 
to install packages as binder launches a session is to include a file recognized by the **pip** package installer, called by convention `requirements.txt`. 
Either of these files can be automatically generated so the finesse is to determine which one to use.


Rule of thumb: Use `pip` if you can; but if it fails then go to `conda`. The latter has *channels* such 
as `conda-forge` that can provide resources that are off the beaten path. From the root directory of the
repository issue

```
$ conda env export
```

to produce the `environment.yml` issue


To see what `requirements.txt` would look like issue


```
$ pip freeze
```

You can direct this into a `requirements.txt` file like so:

```
$ pip freeze > requirements.txt
```

#### Loading data using `postbuild`


flag incomplete: Add a `postbuild` (no extension) file in repo root which includes the necessary `wget` command. 

