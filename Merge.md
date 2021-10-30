# Git Merge

## Get Info

### See diffs between one branch and another branch

For example, after using `git fetch origin`, to see the diffs
between your local `main` branch and `origin/main`, use:

    git diff main origin/main

As another example, before merging `<branch-name>` into the
`main` branch, to see the diffs that will be merged, use:

    git diff <branch-name> main

### View list of files that will be merged

First, fetch refs from origin remote, then use `git log` command:

    git fetch
    git log --stat HEAD..origin

## `merge` command

### Merge commits from one branch into another branch

To merge commits in `<branch-name>` into the `main` branch:

    git checkout main

    git merge <branch-name>

