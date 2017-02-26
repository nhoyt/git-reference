# Git Basics

## Getting Started

### Setting your email address

When you want to use different email addresses for different
repositories, and therefore do not want a globally-defined
default email address, use the following setting in the `[user]`
section of your `$HOME/.gitconfig` file:

    useConfigOnly = true

Alternatively, you can issue the following command:

    git config --global user.useConfigOnly true

This will cause Git to abort commits in any local repos where
you have not configured your email address.

Then, in your local repo, use the following command, which
will update the `local .git/config` file:

    git config user.email <address>

### Using `.gitignore` files

Set global `.gitignore` (in `$HOME`) to exclude `.DS_Store` files

Create local `.gitignore`, especially for npm-based projects,
to exclude `node_modules/` and `.jshintrc`

### When you have multiple remotes, set `remote.pushDefault`

    git config remote.pushDefault <remote>

You must issue the `git config remote.pushDefault <remote>`
command from within the repository to which it applies. For
example, when issued from within submodule `build`, it will
update `../.git/modules/build/config`.

### Using `git pull --rebase`

If you rewrite history, e.g., update `user.email` for commits,
when you pull in the updates, use `git pull --rebase`.

Stack Overflow: "You should use `git pull --rebase` when your
changes do not deserve a separate branch."

### Storing credentials for remote repositories

    git config --global credential.helper osxkeychain

You can also use this type of setting in `~/.gitconfig`:

    [credential "http://git.repo-host.com"]
        username = <username>



## Branch Commands

When you create a new branch, unless you use the `--orphan` switch
you will import all of the files from `master` into the new branch.

### List all branches

    git branch [-v]  # or

    git branch --list [-v]

### Create a new branch

    git branch <new-branch-name>

### Switch to the new branch

    git checkout <new-branch-name>

### Create new branch and checkout in one step

    git checkout -b <new-branch-name>

### Delete a branch

    git branch -d <branch-name>

### Create a new orphan branch and checkout

    git checkout --orphan <new-branch-name>

Then use this command to clear the working directory:

    git rm --cached -r .

NOTE: Issue first commit before switching to another branch or
your changes will (apparently) be lost.



## Remote Commands

### Determine whether there are upstream changes in remotes

    git remote update

This is equivalent to

    git fetch --all

### Fetch a named remote ref into the index

Note: `<remote-name>` is optional if it is `origin`

    git fetch <remote-name>

### View the changes that will be merged after `git fetch`

    git log --stat HEAD..origin

### Determine the URL of remote origin

    git remote show origin

### Determine the URL of another named remote

    git remote get-url <remote-name>

### Push master branch to alternate remote

    git push <alternate-remote> master



## Miscellaneous Commands

### Undo an add command: (e.g. `git add <filename>`)

    git reset HEAD <filename>

### See diffs for already-staged files

    git diff --cached

### See diffs between working copy and previous commit

    git diff <commit-hash> <filename>

### Replace working copy file with version currently in the index

    git checkout -- <filename>

### Replace a working copy file with version from previous commit

    git checkout <commit-hash> <filename>

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



## What certain commands actually do

    git pull  =>  git fetch && git merge

    git remote update  =>  git fetch --all
