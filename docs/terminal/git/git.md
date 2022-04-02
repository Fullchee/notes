---
title: "Git Notes"
date: "2018-08-15"
summary: "Git notes from a while back"
---

## Pull Requests

### Quickly create a PR

```bash
createpr() {
	git stash;
	git switch -c $1;
	git commit --allow-empty --no-verify -m "Trigger GH Actions";
	git push origin $1 --no-verify;
	git set-upstream;
	gh pr create --assignee "@me" --title "[Default Prefix] " --web;
	git stash pop;
}
```

## Undoing

### Undo a `git rm` for a single file
- [[terminal]] `--` is used so any future dashes are considered strings and not flags
- useful when the file path or branch name has dashes
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

### Undo all changes to a repo
```bash
# won't touch unstaged files files
# just sets the staged & committed files to be exactly like origin/master
# will delete any unstaged changes
# Your local repo will also lose all unpushed commits!
# you can may be able to recover unpushed commits via git reflog
git reset --hard origin/master
```

### Move a file from the 'staged' state to 'unstaged' state
`git reset HEAD <file>`

### git-stash

- View all stashes `git stash list`
- Named stash with all staged files: `git stash save "stash name"`
- Named stash with certain files: `git stash push -m <stash_name> <path_to_files>`
- Get the stash changes: `git stash apply <stash name>`
    - stashes are saved in a stack, to apply the previous stash: `git stash pop`
- `git stash drop 0`
    - deletes a stash

### git revert "hash"

- git revert undoes only that provided hash's chnages
- it will still keep the changes of the commits in between
- **set the HEAD as a previous commit**: `git revert --no-commit 0766c053..HEAD`
  - `--no-commit` lets you revert every commit without creating a new commit for each
  - safe, no history change
- git shows `(cherry-or-revert)`, use `git revert --quit`

### `git reset` vs `git checkout`

- reset: move tip of branch (HEAD) to a different commit
  - If A -> B -> C = HEAD and `git reset --hard A`, B and C will be lost
  - git reflog to recover the commits! (quickly! otherwise git might garbage collect)
- staged -> unstaged: git reset -- file
- reset changes the actual

- checkout: switch between branches

#### reset vs checkout on files

- reset: staged snapshot matches the given commit
- checkout: working file matches the given commit

## Conflicts

### git rebase

```bash
git checkout feature
git rebase master
```

**Flatten commits**

1. `git rebase -i HEAD~4` where 4 is the number of commits
2. In the text editor, have the `pick` changed to `squash` or `s` for commits you don't want

### git merge vs git rebase

- like `revert` vs `reset`
- Golden rule of rebasing: **only rebase private branches**
- Merge will create a new commit
- rebase will just move all the branch's new commits to the end of master's HEAD
- `git rebase -i` is really useful for cleaning up private branches

* how to use the merge tool `git mergetool`

### Taking all of their/our changes

- if you're already in a conflict state
  - `git checkout --theirs path/to/file`
  - `git checkout --ours path/to/file`
- pulling theirs: `git pull -X theirs`

## Branching

- **Create a new branch on local** `git checkout -b <branch_name>`
- **List all branches (including local branches)** `git branch -a`
- **Delete a local branch** `git branch -d <branch_name>`
- **Get local branch name** `git rev-parse --abbrev-ref HEAD`
- Rename a branch: `git branch -m <old-name> <new-name>` (m stands for move, mv)

### Remote Branches

- **Create a new branch on a remote** `git push <remote name> <local_branch_name>:<remote_branch_name>`
  - `git push <remote_name> <branch_name>` if the local and remote names are the same
- **Only list remote branches** `git branch -r`
- **Delete a remote branch** `git push <remote_name> --delete <branch_name>`

- `git remote add origin <url`
- git remote set-url \<name\> \<newurl\> [\<oldurl\>]

## Remotes

- add a remote: `git remote add origin git@github.com:User/UserRepo.git`
- change the url of a remote: `git remote set-url origin git@github.com:User/UserRepo.git`

## Git Log

- View all commits that modified a file or a directory `git log --follow <path_to_dir_or_file>`
  - don't use `git log -p`, that shows the entire diff
- Get the SHA of the latest commit that changed a file `git --no-pager log -n 1 --pretty=format:%H -- <path_to_file_or_dir>`

## git diff

- Just get files that changed `git diff --name-status <commit/branch1> <commit/branch2>`

## Locally ignoring

```
git update-index --skip-worktree [<file>...]         (create a git alias <git ignore>)
git update-index --no-assume-unchanged [<file>...]   (create a git alias <git unignore>)
```

## Blame

- **View how one file's changed across time**:

* `git log --follow -p -- file`
* Simpler version that doesn't follow: `git log -p <filename>`

### View the number of commits each person made

`git shortlog -n -s`

## Git Submodules

What are submodules?

- git repos in a git repo
- for example: zprezto uses them

1. Add a submodule `git submodule add <URL to a git repo>`
2. Pulling from a repo with submodules

```bash
git clone <main repo URL>   # won't get submodule contents
cd <main repo dir>
git submodule init          # (like a git fetch, doesn't merge into your
git submodule update        # like git pull for the submodule

# or you could cd into the submodule and run
git pull
```

### Sparse Checkout

```bash
mkdir <repo>
cd <repo>
git init
git remote add -f origin <url>
git config core.sparseCheckout true
```

- If you only want to ignore a single file without adding to the `.gitignore`, add the same structure to the `.git/info/exclude`, same structure as `.gitignore`

### Git search across branches

```
git grep "DialChart" `git show-ref --heads`
```

**If that comes up empty**

```
git grep "DialChart" $(git rev-list --all)
```
### Run a git command in another directory
`git -c <directory> <git_command>`

### Add an executable file

```bash
git add <file>
git update-index --chmod=+x <file>
git add .
```

### Setting up a staging branch
