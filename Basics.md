# Git Basics

## 1. Getting Started

### Cloning a remote repository

Note: For a repository named `<repo-name>.git`, `git clone` will
create a folder named `<repo-name>`:

    cd /path/to/parent/directory/for/working-copy
    git clone https://example.com/<repo-name>.git
    cd <repo-name> # begin working...

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

### Storing credentials for remote repositories

    git config --global credential.helper osxkeychain

You can also use this type of setting in `~/.gitconfig`:

    [credential "http://git.repo-host.com"]
        username = <username>

### When you have multiple remotes, set `remote.pushDefault`

    git config remote.pushDefault <remote>

You must issue the `git config remote.pushDefault <remote>`
command from within the repository to which it applies. For
example, when issued from within submodule `build`, it will
update `../.git/modules/build/config`.

## 2. Init and push local content to empty remote repository

Create local repo if necessary:

    cd /path/to/my/source/files   # cd to directory containing source files
    git init                      # create repo and .git subdirectory with requisite Git files
    git add -A                    # stage all changes
    git commit -m "message"       # commit all changes

Add remote:

    git remote add -m main origin <remote-url>

`push` (first time):

    git push --set-upstream origin main

or equivalent:

    git push -u origin main

## 3. Change history with updated user.email value

See `~/Scripts/git-author-rewrite.sh`

## 4. Change AUTHOR and EMAIL in git history

For the last commit:

    git commit --amend --author="Author Name <email@address.com>"
    git push --force --tags origin 'refs/heads/*'

For the entire history of a branch:

    git filter-branch --commit-filter '
    if [ "$GIT_COMMITTER_NAME" = "<Old Name>" ];
    then
        GIT_COMMITTER_NAME="<New Name>";
        GIT_AUTHOR_NAME="<New Name>";
        GIT_COMMITTER_EMAIL="<New Email>";
        GIT_AUTHOR_EMAIL="<New Email>";
        git commit-tree "$@";
    else
        git commit-tree "$@";
    fi' HEAD

    git push --force --tags origin 'refs/heads/*'
