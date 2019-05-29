## Add an empty directory

This tells git to ignore everything except the `.gitignore` file, which contains these lines:

```
# Ignore everything in this directory
*
# Except this file
!.gitignore
```

via https://stackoverflow.com/questions/115983/how-can-i-add-an-empty-directory-to-a-git-repository


## Patching

    git apply --check tests.patch 
    git apply -v --check tests.patch to see where it's blaring

## Getting LOC changed in a commit range

    git log --author=Brian --since="Feb 15, 2014" --no-merges --numstat --pretty="%H" -- tests | awk 'NF==3 {plus+=$1; minus+=$2} END {printf("+%d, -%d\n", plus, minus)}'
