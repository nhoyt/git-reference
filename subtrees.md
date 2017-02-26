# Git Subtrees

## Adding a subtree

Define a named remote for the subtree's central repository:

    git remote add <remote-name> <remote-URL>

Then fetch the remote ref into the index:

    git fetch <remote-name>

Update the index with the contents of the remote's `master` branch
and (using the `-u` switch) update the working directory as well:

    git read-tree --prefix=<subtree-path> -u <remote-name>/master

The `git status` command will show that the new files have already
been added to the index:

    Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)

Finally, commit the changes:

    git commit -m "Added subtree <subtree-path>"



## Cloning/updating a repository with subtree(s)

Just use the normal Git commands:

    git clone <repo>
    or
    git pull



## Getting an update from the subtree's remote

Update the local cache from the subtree’s remote:

    git fetch <remote-name>

Then do a subtree merge, using a squash commit to avoid merging histories:

    git merge -s subtree --squash <remote-name>/master

The `git status` command will show the changes to be committed...

Commit the updates:

    git commit -m "Updated <remote-name>"

## Backporting to the subtree's remote

From the main development branch, view recent commits:

    git log --oneline --decorate --stat -5

Create a local branch specifically for backporting:

    git checkout -b backport-<remote-name> <remote-name>/master

Then cherry-pick the commits we want to backport:

    git cherry-pick -x --strategy=subtree <commit-hash>

Repeat as necessary...

Finally, view the commits in the backport branch with:

    git log --oneline --decorate --stat -3

And push to the upstream remote-name and branch created when
the subtree was added (see above):

    git push <remote-name> HEAD:master
