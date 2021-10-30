# Git: Misc. Commands

## Syncing a fork with upstream repository

First, create a remote that references the original repo from which
your fork was created:

    git remote add upstream <original-repo-url>

Fetch the branches and their respective commits from the `upstream`
repo:

    git fetch upstream

Checkout your fork's local `main` branch:

    git checkout main

Merge the changes from `upstream/main`:

    git merge upstream/main

If necessary, push the changes to the fork's `origin`:

    git push origin main

## Using `git pull --rebase`

If you rewrite history, e.g., update `user.email` for commits,
when you pull in the updates, use `git pull --rebase`.

Stack Overflow: "You should use `git pull --rebase` when your
changes do not deserve a separate branch."

## What certain commands actually do

    git pull           =>  git fetch && git merge

    git pull --rebase  =>  git fetch && git rebase

    git remote update  =>  git fetch --all

    git remote prune   =>  git fetch --all --prune
