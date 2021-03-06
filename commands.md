# Git Commands and Tips

----------------------------------------------------------------
## Remotes

### List all remotes and their associated URLs

    git remote -v

### Add remote (ssh or http)

    git remote add origin <url>

    git branch --set-upstream-to=origin/master master

### Fetch remote refs into the index

Note: The default for `<remote-name>` is `origin`

    git fetch <remote-name>

### Fetch refs for all remotes

    git fetch --all

### Determine the URL of remote origin

    git remote show origin

### Determine the URL of named remote

    git remote get-url <remote-name>

### Push master branch to named remote

    git push <remote-name> master

----------------------------------------------------------------
## Reset/Revert

### Unstage file that has been staged for commit

After adding `<filename>` to the index with 'git add' command,
you can remove it from the index with:

    git reset HEAD <filename>

### Replace working copy file with version currently in the index

Note: Current version of `<filename>` will be overwritten!

    git checkout -- <filename>

### Reset all working copy files to versions currently in the index

Note: All uncommitted working copy modifications will be lost!

    git reset --hard HEAD

### Replace a working copy file with version from previous commit

Note: Current version of `<filename>` will be overwritten!

    git checkout <commit-hash> <filename>

### Change the last commit message

    git commit --amend -m "New commit message"

### Interactively change the last `<n>` commit messages

Note: This command will invoke your editor, which will provide a list
of the commits you've specified, and where you can mark each according
to the action you want Git to perform:

    git rebase -i HEAD~<n>

### Revert branch (roll back) to previous commit

Note: Using the `--no-commit` option will result in only having to make
a single commit. The `--no-edit` option will result in multiple commits
but will not require adding a commit message for each.

    git revert --no-commit <commit-hash>..HEAD

    git commit

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
## Branching

When you create a new branch, unless you use the `--orphan` switch,
you will import all of the files from your current branch into the
new branch.

### Create new branch

    git branch <branch-name>

### Checkout branch

    git checkout <branch-name>

### Create new branch and checkout in one step

    git checkout -b <branch-name>

### List local branches

    git branch  =>  git branch --list

You can use the -v switch to get information on the commit that HEAD
points to for each branch

### List remote branches

    git branch -r

### List all branches, both local and remote

    git branch -a

### Push local branch to `origin`

    git push -u origin <branch-name>

### Delete a branch locally

    git branch -d <branch-name>

### Delete branch on `origin`

    git push origin --delete <branch-name>

### Delete local branches that are no longer on the remote

Note: The default for `<remote-name>` is `origin`

    git fetch <remote-name> --prune

### Prune branches on `origin` that no longer exist

    git remote prune origin

### Create a new orphan branch and checkout

    git checkout --orphan <new-branch-name>

Then use this command to clear the working directory:

    git rm --cached -r .

NOTE: Issue first commit before switching to another branch or
your changes will (apparently) be lost.

----------------------------------------------------------------
## Merging

### Merge commits from one branch into another branch

To merge commits in `<branch-name>` into the `master` branch:

    git checkout master

    git merge <branch-name>

### See diffs between one branch and another branch

For example, after using `git fetch origin`, to see the diffs
between your local `master` branch and `origin/master', use:

    git diff master origin/master

As another example, before merging `<branch-name>` into the
`master` branch, to see the diffs that will be merged, use:

    git diff <branch-name> master

### View list of files that will be merged

For example, after using `git fetch`, to fetch refs from
origin remote, use:

    git log --stat HEAD..origin

----------------------------------------------------------------
## Miscellaneous

### See diffs for already-staged files

    git diff --cached

### See diffs between working copy and previous commit

    git diff <commit-hash> <filename>

### See diffs between last and previous commits

    git diff HEAD^

### See diffs between two branches

    git diff <branch-1>..<branch-2>

Use `--name-only` switch to only list file names
Use `--dirstat` switch to only list directories

### See diffs for `<filename>` between two branches

    git diff <branch-1>..<branch-2> <path/to/filename>

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

### Delete a tag locally and remote

    git push --delete origin <tag-name>

    git tag --delete <tag-name>

----------------------------------------------------------------
## Syncing a fork

First, create a remote that references the original repo from which
your fork was created:

    git remote add upstream <original-repo-url>

Fetch the branches and their respective commits from the `upstream`
repo:

    git fetch upstream

Checkout your fork's local `master` branch:

    git checkout master

Merge the changes from `upstream/master`:

    git merge upstream/master

If necessary, push the changes to the fork's `origin`:

    git push origin master

----------------------------------------------------------------
## What certain commands actually do

    git pull  =>  git fetch && git merge

    git pull --rebase => git fetch && git rebase

    git remote update  =>  git fetch --all

    git remote prune   =>  git fetch --all --prune
