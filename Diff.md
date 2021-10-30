# Git Diff

## Multiple files

### Working copy files and last commit

    git diff

### Working copy files and already-staged files

    git diff --cached

### Last commit and previous commits

    git diff HEAD^

### Compare two branches

    git diff <branch-1>..<branch-2>

Use `--name-only` option to only list file names and `--dirstat`
option to only list directories.

## Specific file

### `<filename>` and previous commit

    git diff <commit-hash> <filename>

### `<filename>` between two branches

    git diff <branch-1>..<branch-2> <path/to/filename>
