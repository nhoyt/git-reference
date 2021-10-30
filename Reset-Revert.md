# Git Reset & Revert

## Modify the index

### Unstage file that has been staged for commit

After adding `<filename>` to the index with `git add` command,
you can remove it from the index with:

    git reset HEAD <filename>

## Modify working copy file(s)

### Replace working copy file with version currently in the index

Note: Current version of `<filename>` will be overwritten!

    git checkout -- <filename>

### Reset all working copy files to versions currently in the index

Note: All uncommitted working copy modifications will be lost!

    git reset --hard HEAD

### Replace a working copy file with version from previous commit

Note: Current version of `<filename>` will be overwritten!

    git checkout <commit-hash> <filename>

## Modify commit message

### Change the last commit message

    git commit --amend -m "New commit message"

### Interactively change the last `<n>` commit messages

Note: This command will invoke your editor, which will provide a list
of the commits you've specified, and where you can mark each according
to the action you want Git to perform:

    git rebase -i HEAD~<n>

## Undo commits

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
