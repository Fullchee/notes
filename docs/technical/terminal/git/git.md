## Locally ignoring

```
git update-index --skip-worktree [<file>...]         (create a git alias <git ignore>)
git update-index --no-assume-unchanged [<file>...]   (create a git alias <git unignore>)
```

## Blame

-   **View how one file's changed across time**:

*   `git log --follow -p -- file`
*   Simpler version that doesn't follow: `git log -p <filename>`

### View the number of commits each person made

`git shortlog -n -s`

## Git Submodules

What are submodules?

-   git repos in a git repo
-   for example: zprezto uses them

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

-   If you only want to ignore a single file without adding to the `.gitignore`, add the same structure to the `.git/info/exclude`, same structure as `.gitignore`

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
