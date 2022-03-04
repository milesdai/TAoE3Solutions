# Contributing with Github

This project uses a rebase workflow to merge pull requests.
This is a quick guide on how to make changes and submit pull requests.
For a more in-depth tutorial on this process, see this [blog post](https://medium.com/singlestone/a-git-workflow-using-rebase-1b1210de83e5)

## Setup

To contribute to the project, first make a fork of the repo by logging into Github and clicking the fork button in the top right.
This will make a copy of the repo for you to work on in your Github account.
For the sake of this tutorial, let's call this repo `yours`, so the `master` branch on your Github repo will be denoted as `yours:master`.
The main master branch will be denoted as `milesdai:master`.
Next, clone this repository (the fork you just created) onto your computer.
Add another remote called `upstream` that points back to the main repository (e.g. milesdai/TAoE3Solutions).

```shell
# Add upstream remote
git remote add upstream git@github.com:milesdai/TAoE3Solutions.git
```

You are now ready to begin contributing changes.

## Making Changes

These steps should be performed for every contribution you wish to make.
For this workflow, **it is very important to not commit any changes to your `master` branch.**
Instead, let's create a branch called `new-changes`.
Before we do, let's make sure our local master branch is up to date by pulling any changes from upstream (i.e. pull from `milesdai:master`):

```shell
# Pull in upstream changes
# (recall that we set upstream to point to the milesdai/TAoE3Solutions repo in the previous step)
git pull upstream master
# Create a new branch called new-changes
git checkout -b new-changes
```

This will create a new branch called `new-changes` and will switch you to that branch.
You can now make changes and commits as usual.
Try to keep your commits as modular as possible.
For example, one commit per exercise added.

When you are ready to submit your changes, you will submit a pull request (PR).
Before you do though, it is best practice to rebase against an updated version of master.

### Rebasing

*Note: rebasing can get pretty advanced if you are new to Git.*
*If you are uncomfortable with this step, feel free to skip to filing a PR in the next paragraph.*
This is because while you were making your changes, `milesdai:master` may have been updated.
To get these updates run `git fetch upstream master:master`.
This will grab any changes added to `milesdai:master` on Github and add them onto `yours:master` locally.
At this point, your branch (`yours:new-changes`) will be based on an old commit in your master branch.
We will use rebase to fix that.
Run `git rebase master` to rebase against master which has the effect of taking all your commits on your branch and replaying them at the end of the new master branch.
This concept can be very confusing for those new to Git.
To get a better understanding, it can be helpful to read through the blog post linked above as well as this [tutorial on rebasing](https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase).
If any rebase conflicts occur fix them like you would a merge conflict.
Follow the instructions printed on the screen to fix the rebase problems and continue the rebase.

### File a PR

Now, we can file a PR.
To do so, push your branch (`yours:new-changes`) to Github.

```shell
git push -u origin new-changes
```

On Github, you should now see a green button that let's you file a PR.
Click this button, and write a quick description of your PR.
Click submit.
Now you can wait for feedback to see if you need to edit yoru PR.

### Editing a PR

You may want to edit a PR to fix any mistakes or respond to feedback.
To do so, you can make changes in your local copy of the branch and push these changes to Github with `git push`
(using the `-u` flag in the previous step links your local branch to the remote branch, so `git push` knows exactly where to send your pushed branch).

Instead of continuing to add more commits, you can use `git commit --amend --no-edit` to revise your last commit.
The `--no-edit` flag just prevents the text editor from popping up and asking you to revise your commit message.
Now, you can force push to your Github branch with `git push --force`, and everyone will now see the revised version of your PR.

## Merging a PR

If your PR is accepted, the maintainer(s) of the project will merge your PR.
At this point, you can feel free to delete the branch you created for this PR on Github and locally.
Github may offer to delete the branch for you (which you can safely accept), or you can go through the repository settings to delete.
Locally, you can switch to master (`git checkout master`) and use `git branch -d new-changes` to delete your branch.
At this point, you may want to update your local copy of master again with `git pull upstream master`
To make new changes, just repeat the steps starting from the [Making Changes](#making-changes) section.
