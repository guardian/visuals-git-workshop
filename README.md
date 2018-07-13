
**Git Setup**

Check that you have git installed with `git --version`

If you don't have it installed, it will prompt you to do so. [Do it](https://www.atlassian.com/git/tutorials/install-git).


To check that you have it configured properly: `git config --list`

If your user.name and user.email are not there you need to set them:

```
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
```

**What is git, what is it for?**

Git is a version control system. By adding git tracking files to your project you are able to
record a history of the changes that your project will go through.
It allows you to review your changes, see who made the changes, revert them etc.

**Set up a project**

If you are starting a project from scratch:

```
cd your-project-dir
git init
```
That's it! Or you can clone a github repo by doing `git clone <projecturl>` and cd into the dowloaded folder.
Git will already be initialised for the project.

**Staging area**

If you run `git status` you can see all the files that have been modified in red. In order to save a change in git you need to add the file to the staging area `git add yourfilepath/yourfilename`. To remove it from the staging area `git reset yourfilepath/yourfilename` removes the file from the staging area. Your changes are still present locally but won't be tracked/committed. In case you want to track the changes in every file you modify, use `git add -A`.
You can also add changes programmatically by running `git add -p`.

**Commit your changes**

Once you have the correct changes in the staging area you are ready to commit. `git commit -m "your commit message"` will create a commit with a commit message to describe your change.

**Remote repositories**

If you want to track your changes on github repo and did not clone the project from github, to connect your local project to the github repo run `git remote add origin https://github.com/user/repo.git` with the url of the github repo (`git remote -v` to verify the remotes you've just added). At the guardian we use repo genesis(https://repo-genesis.herokuapp.com/) to easily set up a new github project.
If you cloned your repo from github, the project will already be configured with the remotes pointing to that repo.

**Working on branches**

Especially when working on big features that will change the project significantly, it is advised to work on a feature branch, so that a clean, working version of the project (usually on the master branch). NB: when you make a new branch,you create a copy of the branch you are currently working on. You should therefore always branch from master, which should always be up to date.
`git checkout -b thenameofyourbranch` will create a new branch and select it as the branch you are working on.
To select a different branch: `git checkout anotherbranch`

**Pushing your changes**

`git push` will push changes to the remote branch that matches the one you are currently working on locally. You won't be able to push a change if the remote branch's latest commits are more recent than the ones you are trying to push (that can result due to a merge by somebody else collaborating to the repo).

**Pulling changes**

`git pull` will fetch the remote branch and automatically try to merge the changes to your local branch. When you are working on projects with multiple contributors and you start working on a new feature, it is always good to pull the latest version of master and check out a new branch from there, so that you will end up with less conflicts with merging your changes back into master.

**Merging branches and conflicts**

This is how you integrate changes between branches. Usually you'll want to merge your changes from your feature branch to master. Especially when you are working collaboratively on a project, you should first merge the lastest version of master into your own branch (pull master than merge it into your branch) then merge your updated branch into master, to bring your new updates to the main version of the project.

Sometimes git won't be able to merge all your changes automatically and you will incur into merge conflicts. In the cli you will be notified of which files have conflicts that need to be resolved. After you have fixed these conflicts, add your resolving changes in a new commit.

`git merge master` will merge master into your branch.

**Check your history**

`git log` will show you the history of commits for your branch. Each commit has a unique hash used to identify it.

**Github pull requests**

A pull request is just a request to merge your latest changes from a branch to (usually) the master branch on github. GH only allows merging if no conflicts between the branches exist. Therefore you need to resolve your conflicts locally (by merging master into your local feature branch) before pushing to GH and open a PR.


**Typical workflow to keep master clean and avoid a mess**

Get the latest version of master
```
git checkout master
git pull
```

Create a new branch and select it
`git checkout -b mybranch`

Make some changes then add, commit and push

```
git add -A
git commit -m "This message describes my latest changes"
git push
```
When it is time to merge your changes to master

```
git checkout master
git pull
git checkout mybranch
git merge master
```
You might have to fix some conflicts, once you have resolved conflicts in all the files:
```
git add -A
git commit -m "Fix conflicts"
```

Now you can push your changes

`git push`

Then on the github repo you will see your branch and you will be able to open a PR. After reviewing your changes merge into master, then make sure you get the latest version of master on your pc again:

```
git checkout master
git pull
```
And then checkout a new branch and start working on a new feature

`git checkout -b yetanotherbranch`

**Aliases**

If you use Oh my Zsh in your terminal, you can use git aliases to use a shorter syntax for all your git commands
Ie: git status becomes gst, git checkout becomes gco and so on. You can also configure your own aliases.
