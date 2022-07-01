### Switch from `master` to `main` branch

-   https://stevenmortimer.com/5-steps-to-change-github-default-branch-from-master-to-main/
-   git push -u origin main

## Branching

-   **Create a new branch on local**
    -   `git checkout -b <branch_name>`
-   **List all branches (including local branches)**
    -   `git branch -a`
-   **Delete a local branch**
    -   `git branch -d <branch_name>`
-   **Get local branch name**
    -   `git rev-parse --abbrev-ref HEAD`
-   Rename a branch
    -   `git branch -m <old-name> <new-name>`
    -   (m stands for move, mv)

### Remote Branches

-   **Create a new branch on a remote**
    -   `git push <remote name> <local_branch_name>:<remote_branch_name>`
    -   `git push <remote_name> <branch_name>`
        -   if the local and remote names are the same
-   **Delete a remote branch**
    -   `git push <remote_name> --delete <branch_name>`
