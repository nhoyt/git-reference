# Git Submodules

## Adding a submodule

    git submodule add <url> [folder]
    git commit -am "Added submodule [folder]"
    git diff --cached --submodule

## Cloning a repository that has submodules

These three commands:

    git clone <repo-with-submodules>
    git submodule init
    git submodule update

are equivalent to this single command:

    git clone --recursive <repo-with-submodules>

Important notes:

1. Be sure to use one of the above, either `git clone` followed by `git
   submodule init` and `git submodule update`, or `git clone --recursive`,
   to avoid subsequent problems with pushing changes to the submodule.

2. Once you have done one of the above, if you plan to make any changes to
   submodule files, be sure to cd into each submodule folder and checkout
   the `master` branch, e.g.,

    cd <submodule-folder>
    git checkout master

Otherwise you will remain in a detached HEAD state and will not be able to
commit or push changes.

## To make changes in your submodule

First check out a branch (usually `master`).

Important note: If you skip this step, the submodule will remain in a detached
HEAD state.

    cd <submodule-name>
    git checkout master

Then `add`, `commit` and `push` changes to remote.

Finally, `cd` out of the submodule subdirectory to the parent repo working copy:

    cd ..

If you do a `git status` you will see that `<submodule-name>` has been modified.

    git add <submodule-name>
    git commit -m "Updated ..."
    git push

## When ready to push commits in the main project

To check whether submodule commits have been pushed, use:

    git push --recurse-submodules=check

To push commits in the main project and all submodules

    git push --recurse-submodules=on-demand

## To pull the latest changes for both the submodule and the main repo
simultaneously

Use the following command from the parent repo:

    git pull origin <branch-name-of-parent-repo> --recurse-submodules

Assuming the submodule is tracking the master branch, you can add the following
line in your `.gitmodules` file, in the section for the corresponding submodule:

  branch = master

and then use the shorter command (from the parent repo):

    git pull --recurse-submodules

## Updating submodules in your working copy

These two commands:

    git fetch
    git merge origin/master

are equivalent to:

    git submodule update --remote <submodule-name>

The above command(s) will pull in any upstream changes.

## To remove a submodule

Use the following three commands:

    git submodule deinit <submodule-name>
    git rm <submodule-name>
    rm -rf .git/modules/<submodule-name>

## What certain commands actually do:

    git submodule update --remote <submodule-name>  =>
    cd <submodule-name> && git fetch && git merge origin/master
