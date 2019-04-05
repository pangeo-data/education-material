# git and GitHub 

## The top 40 things you need to know about the pangeo approach to source control

***Why do I care about `git`?***

`git` is a Linux command (by definition since it was written by Linus *himself* in 2005) that does source control. 
Source control is a means of tracking how software and other resources evolve within a project. This however is only
the starting point for 'caring about `git`'. You might say that source control is a means of getting organized; and
that being organized is a tenet of participating in the open source ecosystem. An analogy: 
'Before you go drive on the roads make sure you have gas in your car and air in your tires and engine oil and that 
your muffler is not about to fall off.' In like manner: Understanding `git` (and GitHub) is not required but it 
is good common sense if you are interested in participating in the pangeo community.

***How do I learn about `git`?***

`git` is a slightly complicated topic: Using `git` effectively requires you to have a mental picture of how 
`git` works. Since there are a lot of resources for building this picture we do not try to do so here. Rather 
we recommend investing some time in one of these learning paths and putting what you learn into practice as you go... 

- Use a search engine with 'teach me about git source control'
- Go to a Linux command line and enter `git help`
- Check out [this material from Atlassian](https://www.atlassian.com/git/tutorials/what-is-git)
- Try [Free Code Camp](http://freecodecamp.org) (sign-up required)
- ...and there are *many many* other recommendations to be found online; for example on 
[reddit](https://www.reddit.com/r/learnprogramming/comments/66u0v7/what_is_the_best_tutorial_to_learn_both_gitgithub/)

***Why is there a `git` section in pangeo?***

We want to make sure you understand how `git` and `GitHub` are built into the pangeo framework. This also gives us
the opportunity to recommend some good practices for you to adopt. 

***And so on: More questions...***

With cool answers: The interested participant is invited to expand this. My suggestion is the Q/As stay brief
and jaunty and we can put deeper stuff in other locations as needed.

***How do I clone a repository?***

`git clone http://github.com/someuser/somerepo.git` will create a folder on your machine called `somerepo` which
is a file-by-file copy of the repository as hosted at GitHub. 

***Any caveats on this?***

Good question. There is a cool feature of `git` that does create a caveat. Quoting: 

> Git allows you to include other Git repositories called submodules into a repository. ... Git allows 
you to commit, pull and push to these repositories independently. Submodules allow you to keep projects 
in separate repositories but still be able to reference them as folders in the working directory of 
other repositories.

from 
[Using submodules in git, a tutorial from Vogella](https://www.vogella.com/tutorials/GitSubmodules/article.html)

...so the caveat is that in a potential submodule situation you `cd` to the new repository directory -- the one
you just cloned -- and issue the `git` command

```git submodule update --init --recursive```

Furthermore notice this creates an implicit dependency: If your repository has a dependency on a submodule and
if they are not in synch you have a potential breakdown issue. 


***What is a GitHub User?***

***What is a GitHub Organization?***

***What is Public versus Private on GitHub?***

***Why did I get `403: Forbidden` when I attempted to log in to pangeo using my GitHub ID?***
