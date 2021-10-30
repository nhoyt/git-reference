# Git Tags

## List tags

### All tags with first line of annotation

    git tag -n    # -n implies -l

### All tags that match `<reg-exp>` pattern

    git tag -l <reg-exp>

## Create a tag

### Create annotated tag for the latest commit

    git tag -a <tag-name> -m "<comment>"

### Create annotated tag for a previous commit

    git tag -a <tag-name> <commit-hash>

### Push tag to remote repository

    git push origin <tag-name>

### Push all tags to remote

    git push origin --tags

## Delete a tag

### Delete tag locally and on remote

    git tag --delete <tag-name>

    git push --delete origin <tag-name>
