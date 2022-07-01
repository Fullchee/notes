# Working with the remote repo

## Branches

See [branches page](./branches) for anything branch related

## Quickly create a PR

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

## Remotes

-   add a remote: `git remote add origin git@github.com:User/UserRepo.git`
-   change the url of a remote: `git remote set-url origin git@github.com:User/UserRepo.git`

### Setting up a staging branch
