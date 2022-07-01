## Git Log

-   View all commits that modified a file or a directory `git log --follow <path_to_dir_or_file>`
    -   don't use `git log -p`, that shows the entire diff
-   Get the SHA of the latest commit that changed a file `git --no-pager log -n 1 --pretty=format:%H -- <path_to_file_or_dir>`
