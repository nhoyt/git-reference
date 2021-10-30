# Git Remotes

## List / show

### List all remotes and their associated URLs

    git remote -v

### Determine the URL of remote origin

    git remote show origin

### Determine the URL of named remote

    git remote get-url <remote-name>

## Update the index

### Fetch remote refs into the index

Note: The default for `[remote-name]` is `origin`

    git fetch [remote-name]

### Fetch refs for all remotes

    git fetch --all

## Miscellaneous

### Push `main` branch to named remote

    git push <remote-name> main
