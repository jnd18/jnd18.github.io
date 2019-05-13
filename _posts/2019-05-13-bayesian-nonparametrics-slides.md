---
layout: post
title: Nonparametric Bayesian Methods Slides
---
I've uploaded some slides from talks I gave during my Advanced Topics in Applied Statistics course.
Both of the talks were about nonparametic Bayesian methods, which I find quite neat.
The links to the slides are below in case you want to check them out.
The first talk was a shorter one about Gaussian process regression.
I tried to avoid getting bogged down in the math, since I didn't have the time to explain it, so the material is quite light.
Those slides are [here.](http://rpubs.com/jnd18/gpslides)
The second talk was about Dirichlet process clustering.
This one was longer and involved more of the math behind the method, but it is still a non-rigorous overview.
Those slides are [here.](http://rpubs.com/jnd18/dpslides)

I think nonparametric models are really cool, especially Bayesian ones.
Via nonparametric methods you can specify a model with potentially unlimited complexity, and then use the data to inform how complex the fitted model should actually be.
The main difficulty with nonparametric Bayesian models is that first part: specifying a model with potentially unlimited complexity.
This involves placing a prior distribution over an infinite dimensional space.
Besides the fact that it can be really hard even in principle to come up with a sensible prior on these spaces,
this means that you have to use clever math to grab hold of something finite that you (or your computer) can actually work with.
In the case of Gaussian processes, the key insight is that we only need to consider the behavior of the Gaussian process 
on the training points plus finitely many tests points we'd like to know the values of. Then the problem reduces to standard operations on a finite-dimensional Gaussian distribution.
For Dirichlet processes, the key step is integrating out the infinite vector that we could never sample.
Then, we end up with a perfectly finite sampling procedure called the Chinese Restaurant process.
In my talks I tried to focus on those two aspects of the models: How do we place a prior on an infinite dimensional space? And once we have, how do we compute with it?

The second ingredient of nonparametrics, using the data to inform how complex the fitted model should be, is where Bayesian methods really shine.
For more classical nonparametric techniques, this usually involves some kind of cross-validation to tune the model complexity to the data.
Using cross-validation means that you have to fit the model many times over, which can be prohibitively expensive (but usually this is not a big deal).
With Bayesian models, you can either use type II maximum likelihood (aka empirical Bayes aka evidence maximization aka maximum marginal likelihood)
 or put priors on the complexity parameters to get rid of the need for cross-validation.
I touch on this idea briefly toward the end of the Gaussian process talk.
We can select the complexity of the Gaussian process model by maximizing the marginal likelihood of the hyperparameters.
This marginal likelihood has a closed-form gradient, so we can use gradient-based optimization methods, rather than the cruder "try a bunch of values" cross-validation approach.

The relevance vector machine (a little-known cousin of the support vector machine, not mentioned in the slides above)
 uses a similar approach of maximum marginal likelihood to automatically learn good hyperparameter values
via an EM-like algorithm. Thus, it only needs to be fit once, whereas an SVM, which uses cross-validation to choose its hyperparameter values, would be fit once for every hyperparameter 
combination we wanted to investigate.
In the end, this doesn't necessarily make the RVM any better than the SVM as a general-purpose machine learning method (the RVM has other flaws),
but I do find the RVM more elegant in certain ways.

Similarly to the situation with Gaussian processes and relevance vector machines, the Dirichlet process clustering model has a complexity parameter
 ($\alpha$ controls the number of clusters indirectly) that we can account for almost automatically.
I mention this only indirectly in the talk, but it's possible to place a general-enough prior on $\alpha$
 and then just let the machinery of Bayesian inference do its thing without us ever having to decide how many clusters we think there should be.
As with the RVM to SVM comparison, this doesn't necessarily make Dirichlet process clustering the best clustering method,
but I do find this approach very elegant and principled.

If these brief descriptions have piqued your interest in Bayesian nonparametrics, then give the slides a look. 
Both sets of slides have suggestions for further learning resources at end, and of course, it's easy to search the web for more information too.

