## This repository will show you a basic git workflow for individuals or small teams
<img src="https://miro.medium.com/max/1400/1*cEeZ6LnQdQzDk3kX2fKBYg.jpeg" alt="img" style="height: 50px; width:100px;"/>

### In this workflow, we have three branches:
* Master — This branch will have production code only. In other words, anything you push to the master branch better be free of bugs.
* Develop — This branch will be the “live” version of your software. If you are working on a team, this is the branch that developers will push to on a regular basis with new features.
* Feature — This technically is not a single branch because there can be tens, or even hundreds of outstanding feature branches at a given moment depending on the team size. Each feature branch represents a new chunk of code that will eventually be tested and added to the codebase.
  ##### The basic steps in this flow are as follows:
    * Create a new branch from the develop branch and call it something like “feature-<describe feature   
    here, or give it an ID>”
    * Work on your feature, committing to this feature branch
    * Test your feature
    * Merge your feature into the develop branch
    * Delete your feature branch
    * Once enough features have been added, prepare your release
    * When the release is tested and prepped, merge the develop branch into master
    * Tag the master branch commit to the correct version (i.e. v1.1)
    * Repeat
 
 ### Merging Branches Locally 
 * run ```git log --oneline --decorate --graph --all ``` this helps you see all your branches
 * develop is our main working branch and we will want to merge feature branches back into it
   * run ``git branch`` to check which branch your on
   * if your not on dev, switch to develop branch
   * run ```git merge feat2```
   * you have merged feat2 into develop
   * confirm by ```git branch --merged```
   * delete feat2 branch ``` git branch -d feat2```
   * the branch should now be deleted on your local machine
   * make sure you are on the main branch...eg be on master to merge dev into master, be on dev to merge feature into dev...
   
   

 ## Creating a Fork
Whether you're trying to give back to the open source community or collaborating on your own projects, knowing how to properly fork and generate pull requests is essential.

Fork repo by clicking fork button...

## Keeping Your Fork Up to Date

While this isn't an absolutely necessary step, if you plan on doing anything more than just a tiny quick fix, you'll want to make sure you keep your fork up to date by tracking the original "upstream" repo that you forked. To do this, you'll need to add a remote:

1. Clone your fork to local:

git clone git@github.com:YOUR-USERNAME/YOUR-FORKED-REPO.git

2. Add remote from original repository in your forked repository:
```
cd into/cloned/fork-repo
git remote add upstream git://github.com/ORIGINAL-DEV-USERNAME/REPO-YOU-FORKED-FROM.git
git fetch upstream
```
3. Updating your fork from original repo to keep up with their changes:

git pull upstream master


## Doing Your Work

### Create a Branch
Whenever you begin work on a new feature or bugfix, it's important that you create a new branch. Not only is it proper git workflow, but it also keeps your changes organized and separated from the master branch so that you can easily submit and manage multiple pull requests for every task you complete.

To create a new branch and start working on it:

```shell
# Checkout the master branch - you want your new branch to come from master
git checkout master

# Create a new branch named newfeature (give your branch its own simple informative name)
git branch newfeature

# Switch to your new branch
git checkout newfeature
```

Now, go to town hacking away and making whatever changes you want to.

## Submitting a Pull Request

### Cleaning Up Your Work

Prior to submitting your pull request, you might want to do a few things to clean up your branch and make it as simple as possible for the original repo's maintainer to test, accept, and merge your work.

If any commits have been made to the upstream master branch, you should rebase your development branch so that merging it will be a simple fast-forward that won't require any conflict resolution work.

```shell
# Fetch upstream master and merge with your repo's master branch
git fetch upstream
git checkout master
git merge upstream/master

# If there were any new commits, rebase your development branch
git checkout newfeature
git rebase master
```

Now, it may be desirable to squash some of your smaller commits down into a small number of larger more cohesive commits. You can do this with an interactive rebase:

```shell
# Rebase all commits on your development branch
git checkout 
git rebase -i master
```

This will open up a text editor where you can specify which commits to squash.

### Submitting

Once you've committed and pushed all of your changes to GitHub, go to the page for your fork on GitHub, select your development branch, and click the pull request button. If you need to make any adjustments to your pull request, just push the updates to GitHub. Your pull request will automatically track the changes on your development branch and update.

## Accepting and Merging a Pull Request

Take note that unlike the previous sections which were written from the perspective of someone that created a fork and generated a pull request, this section is written from the perspective of the original repository owner who is handling an incoming pull request. Thus, where the "forker" was referring to the original repository as `upstream`, we're now looking at it as the owner of that original repository and the standard `origin` remote.

### Checking Out and Testing Pull Requests
Open up the `.git/config` file and add a new line under `[remote "origin"]`:

```
fetch = +refs/pull/*/head:refs/pull/origin/*
```

Now you can fetch and checkout any pull request so that you can test them:

```shell
# Fetch all pull request branches
git fetch origin

# Checkout out a given pull request branch based on its number
git checkout -b 999 pull/origin/999
```

Keep in mind that these branches will be read only and you won't be able to push any changes.

### Automatically Merging a Pull Request
In cases where the merge would be a simple fast-forward, you can automatically do the merge by just clicking the button on the pull request page on GitHub.

### Manually Merging a Pull Request
To do the merge manually, you'll need to checkout the target branch in the source repo, pull directly from the fork, and then merge and push.

```shell
# Checkout the branch you're merging to in the target repo
git checkout master

# Pull the development branch from the fork repo where the pull request development was done.
git pull https://github.com/forkuser/forkedrepo.git newfeature

# Merge the development branch
git merge newfeature

# Push master with the new feature merged into it
git push origin master
```

Now that you're done with the development branch, you're free to delete it.

```shell
git branch -d newfeature
```
 
**Additional Reading**
* [Atlassian - Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)

**Sources**
* [GitHub - Fork a Repo](https://help.github.com/articles/fork-a-repo)
* [GitHub - Syncing a Fork](https://help.github.com/articles/syncing-a-fork)
* [GitHub - Checking Out a Pull Request](https://help.github.com/articles/checking-out-pull-requests-locally)


## Clear history, remove previous commit, undo to master...
Here you are basically creating a copy of the master branch before the commits, after reseting...
Then you can rename and set the default branch after reset/push. This will clean up any unwanted history... 

- on branch master revert or go back commits...  ~1 - to as many as you need/check with git log
```
git reset --hard HEAD~1    
```
-create a new local branch
-push reset branch to new branch
-go to remote
  -change default branch to new branch
  -delete master branch
  -rename new branch to master

   


