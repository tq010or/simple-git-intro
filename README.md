# simple-git-intro

`git` is a powerful distributed version control tool that track any files (e.g., text, image, videos or even programmes), however, its steep learning curve has not been always friendly to beginners.
This mini-tutorial aims to guide you to use `git` in 10 minutes by explaining some key concepts. It is not comprehensive, but should cover some common scenarios.

> I assume your computer already has `git` installed and you have general computer operation knowledge. For instance, you know how to open a terminal from your Mac/Linux/Windows.

#### Concept 1: `git` tracks your data
Let's assume you have some code and documents in your local file system (e.g., in `/Users/john/hello_world`) and you want to use `git` to manage them.

You can open a terminal and change to `/Users/john/hello_world` and type
`git init`. Basically, it tells `git` "_hey, I need to use version control in this folder_".

Then you need to tell `git` which files you want to put in by typing `git add *`.
It tells `git` "_hey, please track every file in the current folder for your version control_".
Of course, you can add one or a few files by specifying their names, e.g., `git add hw.py` to add `hw.py`

Next you type `git commit -am "First version of my code and data"`, as you can guess, this tells `git` "_hey, I've told you the files I want to put in this version control and please remember them_".

`git` will then echo back your commit message with a unique hash string (
something like this: `e1eff3f0f71c4ea87b50b7df44ada84b490e7577`).
It means "_okay, I will remember current status of your selected files and you can refer them by this unique hash string_".

After you made some changes to your version controlled files and you want to `git` to remember your changes. You do this by typing `git commit -am "My new changes"`.
Again, `git` will reply you with your commit message and a new hash string e.g., `96b7ead` (only show first 7 characters here).

You can keep on making changes and commit them to `git`.
All these changes are remembered in you local `git` version control system.

You can view all versions of your data by typing `git log`, `git` will then show your commits (including commit timestamp, message and the unique hash string).

You can also change to previous versions by typing `git checkout e1eff3f0f71c4ea87b50b7df44ada84b490e7577` to view and modify files back then.

So far, all your changes are recorded in `git`'s default location, also know as the `master` branch. I will explain `branch` in the next concept.

#### Concept 2: `git branch` and `git merge` for change management
When you want to try many different things on your code and don't want to modify the current version in `master`, you can leverage the `branch` feature in `git`.

By typing `git branch`, you ask `git`, "_hey, what are current available branches in current version control?_".

`git` then replies you a list of `branches`. If you haven't created any `branch` before, you shall only see a default `master` branch where you are currently on.

You can create a branch by `git branch demo`. It means "_hey, plase create a branch and name it with demo_".

If you ask `git` again for available branches by `git branch`, you will then see both `master` and `demo`, so far you are still on `master` branch.

Next you switch to `demo` branch by typing `git checkout demo`.
This command looks familiar, isn't it? You did it when you switched to a previous version.

It is the same idea for `branch`, you switch to `demo` branch and make changes there, `git` will track your changes in that branch.
The advantage is you can create many branches and try different thing there in parallel without worrying about these changes affecting your data in the `master` branch.

You can imagine a typical scenario that many engineers develop their work in their own branch in parallel, when they finish the work, they can `merge` their changes to `master` so that all changes are incorporated in `master` branch.

Suppose I finished my development in `demo` and commit changes by `git commit -am "Dev for DB is done"`.
I then switch back to `master` branch and merge my development in `demo` by typing `git merge demo`.

Then your changes in `demo` will be incorporated in `master`.

If we take a bird view for `git` change management: We create and switch to new branches for parallel development. Once they are done with commits, we merge these developments to `master` branch to ensure all changes are recorded in `master` for further development.
 
#### Concept 3: `git pull` and `git push` for collaborations.
So far all your version control and changes are made in local. It is fine if you are the only developer for your project, but in real world, you may need to work with other ppl.

`git pull` and `git push` are the two commands you use to interact with other ppl's work.

Let's start with `git push` first. You have made a few changes in `master` and you have merged your changes from `demo` to `master`. You want to put your contribution to a shared remote location (e.g., often a repository in github.com), so that other ppl can view and modify them.

You type `git remote add origin https://github.com/john/hello_world`. 
This tells `git`, "_hey, I'd like to have my version control in the remote repository as well, please set up a version control project in github.com under user john and project name hello\_world _".

After that you type `git push`, `git` will then push your current changes in current branch to the remote repo you specified.
Now the remote repo will contain your latest changes in version control.

`git pull` is similar, `git` pulls data from the `remote` repo you specified. When you are developing something with other ppl, they have `pushed` their changes to the remote repo, you can get their changes to your local by typing `git pull`.

In most cases, their changes and your local changes can be merged automatically. 
If auto merge failed, you then need to manually choose which version to use and delete the undesired part in the data.

Having manually resolved merge failure, you need to do another `git commit -am "Manual merge"`, as you made new changes relative to both `local` and `remote` `git` repo.


#### Concept 4: Change status in `git`
From time to time you execute the above commands, you may encounter conflict errors.
I'd suggest we understand the status of `git` changes.
1. Uncommitted vs Committed:
When you made some changes, only if you `git commit` them to local version control that `git` can remember them.
If you make changes and forget to commit them, these changes are not recognised.
You can use `git diff` to show whether there are uncommitted changes in your current branch.

1. Tracked vs UnTracked:
If you added a file into version control (e.g., `git add hw.py`), it is a tracked file.
Other files in the same `git` controlled folder are untracked.
You can use `git status` to view tracked and untracked files.

1. Local vs Remote:
As you can imagine there will be different versions in a multi-user environment.
You `local` commits may be ahead or behind of the `remote`.
If `local` is ahead of `remote`, you can `git push` to incorporate your changes to `remote` servers.
If `local` is behind of `remote`, you can `git pull` to other ppls' changes to `local`.

#### Recipe 1: Create a new repo in remote server and set it up in local git
```
# Suppose you already created project in github or bitbucket
$ git clone git@github.com:john/hello_world.git
```
#### Recipe 2: Create a new repo in local git and set it up in remote server
```
# Suppose you already in the folder
$ git init
$ git add *
$ git commit -am "Init commits"
$ git remote add origin git@github.com:john/hello_world.git
```
#### Recipe 3: Add existing project in local git and set it up in remote server
```
$ git remote add origin git@github.com:john/hello_world.git
```
#### Recipe 4: Ignore all my local uncommitted changes
```
git reset --hard
```
#### Recipe 5: Ignore all my local committed changes and let the latest remote version to overwride my local version
```
git reset --hard
git pull

```
#### Recipe 6: Remove a file that is currently in git
```
git rm hw.py
```
#### Recipe 7: Freeze my current development in this branch, allow me to sth else in other branch, I need to come back to this branch and continue to work from where I left.
```
git stash
git checkout YOUR_BRANCH
# do something
git commit -am "some side work"
git checkout PREVIOUS_BRANCH
git stash apply
```

#### FAQ
1. For quick trouble shooting, I found this cheat sheet is useful:
https://github.github.com/training-kit/downloads/github-git-cheat-sheet.pdf

