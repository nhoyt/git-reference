# Git Basics

## Creating a remote repository on WebFaction

Go to `repos` directory on webfaction

    cd $HOME/webapps/git/repos

Create bare repository

    git init --bare <repo-name>.git

Enable HTTP push

    cd <repo-name>.git
    git config http.receivepack true

## Pushing local content to (empty) remote repository after init

Create local repo if necessary

    cd /path/to/my/source/files   # cd to directory containing source files
    git init                      # create repo and .git subdirectory with requisite Git files
    git add -A                    # stage all changes
    git commit -m "message"       # commit all changes

Add remote

    git remote add -m master origin http://git.relegant.com/<repo-name>.git

`push` (first time)

    git push --set-upstream origin master

or equivalent:

    git push -u origin master

## Cloning a remote repository

`git clone` will create subdirectory named `<repo-name>`

    cd /path/to/parent/directory
    git clone http://git.relegant.com/<repo-name>.git
    cd <repo-name> # begin working...

## Change history with updated user.email value:

See https://help.github.com/articles/changing-author-info/
and `~/Scripts/git-author-rewrite.sh`

## Changing AUTHOR and EMAIL in git history

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

## Using Git with a remote SVN repository

Clone remote SVN repository:

    git svn clone https://yoursvnserver/path

Make some changes, then stage them (`add -A` stages all changes):

    git add -A

You can stage individual files too or use `git add -i` for interactive adding.

    git add <filename>    # repeat as necessary

Commit all staged changes

    git commit -m "commit message"

Commit all local commits back to the SVN repository

    git svn dcommit
