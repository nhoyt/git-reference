# Git Commands and Tips

----------------------------------------------------------------
## Remotes

### List all remotes and their associated URLs

    git remote -v

### Fetch remote refs into the index

Note: The default for `[remote-name]` is `origin`

    git fetch [remote-name]

### Fetch refs for all remotes

    git fetch --all

### View the changes that will be merged after `git fetch`

    git log --stat HEAD..origin

### Determine the URL of remote origin

    git remote show origin

### Determine the URL of named remote

    git remote get-url <remote-name>

### Push master branch to named remote

    git push <remote-name> master

----------------------------------------------------------------
## Undo/Reset

### Undo an add command: (e.g. `git add <filename>`)

    git reset HEAD <filename>

### Undo the last commit

To leave files as they are, but revert the index:

    git reset HEAD~1

To leave files and index as they are:

    git reset --soft HEAD~1

To revert files and index:

    git reset --hard HEAD~1

### Undo all commits back to a fixed point in the history

    git reset --hard <commit-hash>

    git push origin -f master:master

----------------------------------------------------------------
## Branching & Merging

When you create a new branch, unless you use the `--orphan` switch,
you will import all of the files from your current branch into the
new branch.

### Create new branch

    git branch <branch-name>

### Checkout branch

    git checkout <branch-name>

### Create new branch and checkout in one step

    git checkout -b <branch-name>

### Merge commits in <branch-name> into `master`

    git checkout master

    git merge <branch-name>

### Delete a branch

    git branch -d <branch-name>

### Delete branch on origin remote

    git push origin --delete <branch-name>

### Delete local branches that are no longer on the remote

Note: The default for `[remote-name]` is `origin`

    git fetch [remote-name] --prune

### Create a new orphan branch and checkout

    git checkout --orphan <new-branch-name>

Then use this command to clear the working directory:

    git rm --cached -r .

NOTE: Issue first commit before switching to another branch or
your changes will (apparently) be lost.

### List local branches

    git branch  =>  git branch --list

You can use the -v switch to get information on the commit that HEAD
points to for each branch

### List all branches, both local and remote

    git branch -a

----------------------------------------------------------------
## Miscellaneous

### Replace working copy file with version currently in the index

    git checkout -- <filename>

### Replace a working copy file with version from previous commit

    git checkout <commit-hash> <filename>

### See diffs for already-staged files

    git diff --cached

### See diffs between working copy and previous commit

    git diff <commit-hash> <filename>

### Using `git pull --rebase`

If you rewrite history, e.g., update `user.email` for commits,
when you pull in the updates, use `git pull --rebase`.

Stack Overflow: "You should use `git pull --rebase` when your
changes do not deserve a separate branch."

----------------------------------------------------------------
## Tagging

### List all tags

    git tag

### List all tags that match a pattern

    git tag -l <reg-exp>

### Create annotated tag for the latest commit

    git tag -a <tag-name> -m "<comment"

### Create annotated tag for a previous commit

    git tag -a <tag-name> <commit-hash>

### Push tag to remote repository

    git push origin <tag-name>

### Push all tags to remote

    git push origin --tags

----------------------------------------------------------------
## What certain commands actually do

    git pull  =>  git fetch && git merge

    git pull --rebase => git fetch && git rebase

    git remote update  =>  git fetch --all

    git remote prune   =>  git fetch --all --prune
