# git and GitHub 

## Top 40 things to know about the pangeo approach to source control

If you are interested in how pangeo *works* as a technical framework: `git` is integral to the system
and so you'll need to know a fair amount about it. If you are interested in using a pangeo system for
research -- and never mind the underlying motors and gears -- then you will be fine with a working 
familiarity with `git`. We provide the following FAQ-style overview to help you calibrate your `git` picture.
This is nowhere near as constructive -- if you want to learn `git` -- as making time to go through a good
tutorial like the one provided by [software carpentry](https://swcarpentry.github.io/git-novice/).

***What's the (short summary please) main thing I need to know here?***

We figure you are most likely a ***Pangeo User***: You want to do large-scale-data (geo)science on a 
system that provides matching compute power on demand, appropriate tools, data access, manageable cost
and reproducibility. *Reproducibility* includes *code security*: Everything is backed up (regardless of
if you lost your laptop on the bus). In order to participate in this environment you will need a working 
familiarity with `git`. You are the person this FAQ was primarily written for. A ***Pangeo Builder*** or 
***Pangeo Developer*** will need a much deeper engagement with `git` and `GitHub` in relation to the rest 
of the pangeo machinery.


***Why do I care about `git`?***

`git` is a Linux command (by definition since it was written by Linus *himself* in 2005) that does source control. 
Source control is a means of tracking how software and other resources evolve within a project. This however is only
the starting point for 'caring about `git`'. You might say that source control is a means of getting organized; and
that being organized is a tenet of participating in the open source ecosystem. An analogy: 
'Before you go drive on the roads make sure you have gas in your car and air in your tires and engine oil and that 
your muffler is not about to fall off.' In like manner: Understanding `git` (and GitHub) is not required but it 
is good common sense if you are interested in participating in the pangeo community.

(By the way we concede that `git` is a software system and *not* technically a part of `Linux`.)

***How do I learn about `git`?***

`git` is a slightly complicated topic: Using `git` effectively requires you to have a mental picture of how 
`git` works. Since there are a lot of resources for building this picture we do not try to do so here. Rather 
we recommend investing some time in one of these learning paths and putting what you learn into practice as you go... 

- Immerse in the [Software Carpentry git training](https://swcarpentry.github.io/git-novice/)
- Use a search engine with 'teach me about git source control'
- Go to a Linux command line and enter `git help`
- Check out [this material from Atlassian](https://www.atlassian.com/git/tutorials/what-is-git)
- Try [Free Code Camp](http://freecodecamp.org) (sign-up required)
- ...and there are *many many* other recommendations to be found online; for example on 
[reddit](https://www.reddit.com/r/learnprogramming/comments/66u0v7/what_is_the_best_tutorial_to_learn_both_gitgithub/)

***Why is there a `git` section in pangeo?***

We want to establish how `git` and `GitHub` are built into the pangeo framework. This also gives us
an opportunity to recommend good practices. 



***Why do I care about GitHub?***

> GitHub is a web-based hosting service for version control using Git ([Wikipedia](https://en.wikipedia.org/wiki/GitHub))

There are two good reasons to value GitHub. First: Use of GitHub including many bonus features
at the base or entry level is free. Second: If your laptop is eaten by a llama who then falls 
into a volcano: You are out the cost of the laptop but your code is safely preserved on GitHub; 
so you need not panic.

The pangeo code base is distributed across multiple repositories at GitHub. 

***What is a GitHub User?***

A GitHub User is what you want to be! (if you buy into this whole open source / git business). It is a membership
in GitHub that is free and requires you to establish a Username. Once you are a GitHub User you can start creating 
repositories on GitHub. (You can create repositories on your own machines using the `git` command; GitHub need not be involved.)


***What is a GitHub Organization?***

A GitHub organization such as pangeo is a multi-participant version of a GitHub User.  


***If I put my code on GitHub can't somebody else steal it and use it?***

Yes. GitHub is an open source community where the base usage tier is Public. You can pay a modest fee to make your
presence on GitHub Private; whereupon your content will not be visible to anyone unless you grant them access to it.


***What is Public versus Private on GitHub?***

Answer needed.


***Why did I get `403: Forbidden` when I attempted to log in to pangeo using my GitHub ID?***

As a GitHub User your content may be public but you can still be contextually set to Private
in an organization you belong to. So you probably got the 403 because Scott forgot to tell you that 
you need to make your GitHub *membership* in the pangeo organization **public**. 


***Is GitHub -- as it seems -- a static entity; like a file system that stores older versions of itself?***

This question amounts to asking whether code at GitHub is ever *executable on GitHub*. Yes it is. And this 
is a very central feature of GitHub that we just touch on here, beginning with the ubiquitous `README.md` 
file. This file is text interpreted as Markdown (hence the `.md` file extension) that renders in a
formatted and hopefully more readable manner. But this is only the tip of the iceberg as far as 
GitHub *executability*. 


***Why and how do I clone a repository?***

The basic use case is creating a local copy (clone) of a GitHub repo on your local machine where you can
more readily modify and develop the content. From a suitable parent directly the command 

```
git clone http://github.com/someuser/somerepo.git
``` 

will create a folder on your machine called `somerepo` which is a verbatim copy of the repository as hosted at 
GitHub. To synch subsequent modifications with the GitHub version: See below. 


***Any caveats on cloning?***

Good question. There is a cool feature of `git` that does create a caveat. Quoting: 

> Git allows you to include other Git repositories called submodules into a repository. ... Git allows 
you to commit, pull and push to these repositories independently. Submodules allow you to keep projects 
in separate repositories but still be able to reference them as folders in the working directory of 
other repositories.

from 
[Using submodules in git](https://www.vogella.com/tutorials/GitSubmodules/article.html),
a tutorial from Vogella

...so the caveat is that in a submodule situation you `cd` to the new repository directory -- the one
you just cloned -- and issue:

```
git submodule update --init --recursive
```

Notice that if your repository has a dependency on a submodule and
if this not up to date you have a potential breakdown. 

***How do I synch my local clone of a repo with my GitHub version?***

If one is a `git` [Philistine](https://en.wikipedia.org/wiki/Philistinism) like me
one memorizes four commands, issued from the root directory of the repo:


```
git pull
git add .
git commit -m 'comment on what i just did'
git push
```

***Is there a caveat to 'just use these four commands'?***

Yes, a huge caveat. Not knowing more about `git` will eventually put you at risk of wasting time and 
even losing good work (yours or worse: someone else's). Let's elaborate a bit...

- As noted: Carefully going through [software carpentry on git](https://swcarpentry.github.io/git-novice/)
teaches *why* these work, what can go awry, how to deal, and bonuses like how to avoid typing in your 
Username and Password every time you do `git push`.
- If you do not understand *branches* you may clobber content and set back progress
- If you are working from a fork of a repository these commands are inadequate (see 'pull request').
- Anything else to add here?

