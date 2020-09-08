## This repository will show you a basic git workflow for individuals or small teams

### In this workflow, we have three branches:
* Master — This branch will have production code only. In other words, anything you push to the master branch better be free of bugs.
* Develop — This branch will be the “live” version of your software. If you are working on a team, this is the branch that developers will push to on a regular basis with new features.
* Feature — This technically is not a single branch because there can be tens, or even hundreds of outstanding feature branches at a given moment depending on the team size. Each feature branch represents a new chunk of code that will eventually be tested and added to the codebase.
##### The basic steps in this flow are as follows:
* Create a new branch from the develop branch and call it something like “feature-<describe feature here, or give it an ID>”
* Work on your feature, committing to this feature branch
* Test your feature
* Merge your feature into the develop branch
* Delete your feature branch
* Once enough features have been added, prepare your release
* When the release is tested and prepped, merge the develop branch into master
* Tag the master branch commit to the correct version (i.e. v1.1)
* Repeat

