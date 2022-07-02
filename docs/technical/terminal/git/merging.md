# Merging

### git rebase

```bash
git checkout feature
git rebase master
```

**Flatten commits**

1. `git rebase -i HEAD~4` where 4 is the number of commits
2. In the text editor, have the `pick` changed to `squash` or `s` for commits you don't want

### git merge vs git rebase

-   like `revert` vs `reset`
-   Golden rule of rebasing: **only rebase private branches**
-   Merge will create a new commit
-   rebase will just move all the branch's new commits to the end of master's HEAD
-   `git rebase -i` is very useful for cleaning up private branches

*   how to use the merge tool `git mergetool`

### Taking all their/our changes

-   if you're already in a conflict state
    -   `git checkout --theirs path/to/file`
    -   `git checkout --ours path/to/file`
-   pulling theirs: `git pull -X theirs`
