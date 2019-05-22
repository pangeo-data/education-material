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

### What is my pod's name?

You obtain a list of names from the bash prompt like this: 

```
kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}'
```

## binder

## colab

## jupyter hub
