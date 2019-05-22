# pod

## Introduction

When we land in a Jupyter notebook environment -- whether on **binder** or **colab** or a **JupyterHub** -- we are
apt to ask 'Just where am I right now?' This document answers that question in the practical sense of implications. 

## general remarks

A pod can be thought of as a computer with a built-in environment. It may persist or it may evaporate so it is 
important to know what type of environment one is dealing with. An important corollary idea is that pods are often
created on clusters which are in turn orchestrated (turned on, turned off, configured, managed, ...) using a
software framework called `kubernetes`. We can say that a kubernetes cluster has an interaction *command* which 
is `kubectl`. I like to pronounce this **koo - beck - tile** just to annoy people. In what follows when you see
a command that begins with `kubectl` you know it is about interacting with a cluster of computers that can host
pods. 

## pod horsepower

How powerful / wimpy is my computing environment? 
### What is my pod's name? How much memory does it have? What else can I learn about it? 

You obtain a list of names from the bash prompt like this: 

```
kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}'
```

Memory: 

```
kubectil top pod <pod-name-from-above>
```

Or open a Python cell in a Jupyter notebooks and run this: 

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

The output is something like this: 

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

### How much disk space does my pod have? 




## binder

## colab

## jupyter hub
