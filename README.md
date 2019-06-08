# simple-git-intro

`git` is a powerful distributed version control tool, however, its steep learning curve has not been always friendly to beginners.
This mini-tutorial aims to guide you to use `git` in 10 minutes. It is not comprehensive, but should cover many common scenarios.

> I assume your computer already has `git` installed and you have general computer operation knowledge. For instance, you know how to open a terminal from your Mac/Linux/Windows.

## Master `git` by understanding key concepts
#### Concept 1: `git` tracks your data (software code and documents).
Let's assume you have some code and documents in your local file system (e.g., in `/Users/john/hello_world`) and you want to use `git` to manage them.

You can open a terminal and change to `/Users/john/hello_world` and type
`git init`. Basically, it tells `git` "_hey, I need to use version control in this folder_".

Then you need to tell `git` which files you want to put in by typing `git add *`.
It tells `git` "_hey, please track every file in the current folder for your version control_".

Next you type `git commit -am "First version of my code and data"`, as you can guess, this tells `git` "_hey, I've told you the files I want to put in this version control and please remember them_".

`git` will then echo back you commit message and a unique hash string,
something like this: `e1eff3f0f71c4ea87b50b7df44ada84b490e7577`.
It means "_okay, I will remember current status of your selected files and you can refer them by this unique hash string_".

Next when you decided to make some changes to your version controlled files and you want to `git` to remember your changes. You do this by typing `git commit -am "My new changes"`.
Again, `git` will reply you with your commit message and a new hash string e.g., `96b7ead` (only show first 7 characters here).

You can keep on making changes and commit them to `git`.
All these changes are remembered in you local `git` version control system.

You can change to previous versions by typing `git checkout e1eff3f0f71c4ea87b50b7df44ada84b490e7577` to view and modify files back then.

So far, all your changes are recorded in `git`'s default location, also know as the `master` branch. I will explain `branch` in the next concept.

#### Concept 2: `git branch` and `git merge` for change management
When you want to try many different things on your code and don't want to modify the current version in `master`, you can leverage `branch` feature in `git`.

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

 
#### Concept 3: `git pull` and `git push` collaborations.


#### Concept 4: 



## Git FAQ (x minute)
1. Quick trouble shooting
First, use `git branch` to check your local branch,
then use `git log` to check the commit history,
then use `git status` to check file changes
then use `git diff` to inspect changes made so far


