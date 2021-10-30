# Git Branches

## Create / checkout

When you create a new branch, unless you use the `--orphan` switch,
you will import all of the files from your current branch into the
new branch.

### Create new branch

    git branch <branch-name>

### Checkout branch

    git checkout <branch-name>

### Create new branch and checkout in one step

    git checkout -b <branch-name>

### Push new local branch to `origin`

    git push -u origin <branch-name>

## List branches

### Local branches only

    git branch  =>  git branch --list

You can use the -v switch to get information on the commit that HEAD
points to for each branch

### Remote branches only

    git branch -r

### All branches — both local and remote

    git branch -a

## Delete a branch

### Delete local branch

    git branch -d <branch-name>

### Delete branch on `origin`

    git push origin --delete <branch-name>

### Delete local branches that are no longer on the remote

Note: The default for `[remote-name]` is `origin`

    git fetch [remote-name] --prune

## Misc. Commands

### Create a new orphan branch and checkout

    git checkout --orphan <new-branch-name>

Then use this command to clear the working directory:

    git rm --cached -r .

NOTE: Issue first commit before switching to another branch or
your changes will (apparently) be lost.

### Rename `master` branch to `main`

Change directory to local working copy and checkout 'master'

    cd path/to/my-project
    git checkout master

Make sure 'master' branch is up to date

    git fetch -p
    git pull
    git push

Rename the local branch

    git branch -m master main

    # Output of status will show that 'main' branch is still tracking the remote 'master'

    git status
    .. On branch main ... Your branch is up to date with 'origin/master'

Push the renamed 'main' branch and reset the upstream branch

    git push -u origin main

Update the default branch on GitHub

    In Settings > Branches > Default branch

    1. Don't click the 'pencil' icon to 'Rename branch'
    2. Instead, click the 'arrows' icon to 'Switch to another branch'
    3. Select the 'main' branch and then select 'Update'

Delete the master branch on remote (from local working copy)

    git push origin --delete master
