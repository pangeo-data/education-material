# pod

## Overview

When we land in a Jupyter notebook environment -- say **binder** or **colab** or a **JupyterHub** etc --
we can ask 'Just where am I right now?' This document answers that question with practical implications. 
Let's begin with a little joke: "You are standing in a **pod** at the end of a road before a small brick building.
Around you is a forest.  A small stream flows out of the building and down a gully."

Ok *actually* a pod can be thought of as a computer with a built-in working environment. When we use a computer 
we are 
accustomed to stopping at some point (say for lunch) and coming back later. The computer is still
there. However a pod is a construct *on* some computer; and so the question of its persistence is very
important. A pod may persist for days or weeks or indefinitely; or on the other hand it may evaporate in a 
matter of minutes or hours if you stop using it.  If it persists it probably still stops from time to time
and must be re-started. 

### Get pod parameters using Python

Work in progress; need to add disk space bit...

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
        response += "it's running since %s. \n" % running_since
        return response 
    
print(tell_system_status())
```

The output will be something like this: 

```
I am currently running on Linux version 4.14.106.  
This system is named jupyter-robfatland 
It has 8 CPU cores.  
It has 30 Gigabytes of RAM.  
Current disk_percent is 24.4 percent.  
Current CPU utilization is 0.0 percent.  
Current memory utilization is 11.8 percent. 
it's running since Tuesday 23. April 2019.
```

Caveat: This is for the node (EC2 virtual machine) that the pod lives on, not the pod resource limits identified in the 
JupyterHub config (see below). The effective resources available in the *pod* are about 1/2 of the what is printed above 
as we have been placing two user pods on every virtual machine. 


### ***Pro Tip: using `kubectl` and JHub config***

Pods are often created on clusters which are in turn orchestrated (turned on, turned off, 
configured, managed, ...) using a software framework called `kubernetes`. We can say that a kubernetes cluster has 
an interaction *command* which is `kubectl`. I like to pronounce this **koo - beck - tull** but that is no doubt 
incorrect. A shell command that begins with `kubectl` is an interaction with a cluster of 
virtual machines that host pods. For example: Obtain a list of pod names from the bash prompt: 

```
kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}'
```
Then request how much RAM is available:
```
kubectil top pod <pod-name-from-above>
```

Another technical approach: Check the information is available in the 
[JupyterHub config](https://github.com/pangeo-data/pangeo-cloud-federation/blob/eef3a575973f9789bcdb496b794e2334a88b4661/deployments/nasa/config/common.yaml#L59-L64)


## binder

I want my repository to be available in binder! My repo (on GitHub) is called `badger` and my GitHub 
username is `norbert314`. I want to use the `master` branch of this repo. I want to make use of the `mybinder.org` binder
service. This is sufficient information; I now have two paths that I can follow. On the first path I simply use
the wizard provided at the [binder.org website](https://mybinder.org). This is a manual process and when
completed I will find myself in a binder session with a copy of my repository present. 


The second path has two improvements over the first. First I will install a *badge* directly into my 
repository `badger` which will auto-launch the repository (`badger`) in binder. That is: The ***open in binder*** 
badge will work within my repo for anyone to use. We'll call this Cool Feature 1. Secondly we want the
binder session to pre-install software packages that are used by the code in my repository. That
will be Cool Feature 2. 

### Cool Feature 1

To get the launch badge working: Edit the main `README.md` file at the root of your repository 
to include this line at the top of the file:

```
[![Binder](http://mybinder.org/badge.svg)](https://mybinder.org/v2/gh/norbert314/badger/master)
```

To unpack the URL a bit further: Notice this is binder version 2 (`v2`) and that the repo is hosted on GitHub (`gh`). 
To further illustrate the mapping from nouns to markdown: The pangeo organization maintains its own binder
instance called `binder.pangeo.io`. Within the GitHub website `https://github.com` we find that pangeo has
an organization named `pangeo-data`. Therein resides a repository called `pangeo-example-notebooks` where again
we wish to use the `master` branch. This repository has a binder badge in its `README.md` file that reads as follows: 

```
[![Binder](http://binder.pangeo.io/badge.svg)](http://binder.pangeo.io/v2/gh/pangeo-data/pangeo-example-notebooks/master)
```

At the very end of both of these URLs we *could* append `?urlpath=lab`. This is a key-value pair that translates
as "When all is said and done setting up this binder instance: Append `lab` to the binder URL." This has the effect
of establishing the working environment inside [**JupyterLab**](https://jupyterlab.readthedocs.io) which is the
very cool next-generation Jupyter notebook environment. This is an example of where the sidewalk ends: Going into
additional key-value pair features of this binder interface is out of scope. 


Now that we have installed the badge line in `README.md` we are half way done. The other thing that we need 
is a text file in this same repository that describes the computing environment in terms of software packages. 


### Cool Feature 2

There are (for our purposes) a couple of ways to direct the installation of software packages for Python. 
Other languages like **R** have similar mechanisms not described here. The first way is to include a file
recognized by the **conda** package manager, called by convention `environment.yml`. The second way is to 
include a file recognized by the **pip** package installer, called by convention `requirements.txt`. 
Either of these files can be automatically generated so the finesse is to determine which one to use.



## colab

## jupyter hub
