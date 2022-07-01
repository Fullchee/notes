---
title: "Git Notes"
date: "2018-08-15"
summary: "Git notes"
---

## Undoing

### Undo a `git rm` for a single file

-   terminal: `--` is often used
    -   any future dashes are considered strings and not flags
-   useful when the file path or branch name has dashes
    -   `git reset -- my-file.txt`
    -   `git reset my-file.txt`
        -   will think `-f` is a flag

```bash
undo-rm() {
	filePath="$1"
	git reset -- $1
	git checkout -- $1
}
```

### Undo all changes to a single file

```bash
git checkout <commit> <path/to/file>
```

### Make the local repo exactly like remote

```bash
git reset --hard origin/main
```

-   won't touch unstaged files files
-   may be able to recover unpushed commits via git reflog

### Move a file from the 'staged' state to 'unstaged' state

`git reset HEAD <file>`

### git-stash

-   View all stashes `git stash list`
-   Named stash with all staged files: `git stash save "stash name"`
-   Named stash with certain files: `git stash push -m <stash_name> <path_to_files>`
-   Get the stash changes: `git stash apply <stash name>`
    -   stashes are saved in a stack, to apply the previous stash: `git stash pop`
-   `git stash drop 0`
    -   deletes a stash

### git revert "hash"

-   git revert undoes only that provided hash's changes
-   it will still keep all the other commits' changes
-   **set the HEAD as a previous commit**: `git revert --no-commit 0766c053..HEAD`
    -   `--no-commit` lets you revert every commit without creating a new commit for each
    -   safe, no history change
-   git shows `(cherry-or-revert)`, use `git revert --quit`

### `git reset` vs `--hard`

-   staged -> unstaged: git reset -- file

#### `--hard`

-   move tip of branch (HEAD) to a different commit
    -   A -> B -> C = HEAD
    -   `git reset --hard A`
    -   B and C will be lost
    -   git reflog to recover the commits!
        -   (quickly! otherwise git might garbage collect)

![](https://i.stack.imgur.com/qRAte.jpg)

#### reset vs checkout on files

-   reset: staged snapshot matches the given commit
-   checkout: working file matches the given commit

## git diff

-   Just get files that changed `git diff --name-status <commit/branch1> <commit/branch2>`
