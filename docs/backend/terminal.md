https://explainshell.com/explain?cmd=%s
`tldr`

https://bash3boilerplate.sh/
* has best practices

### SSH

```bash
# ssh to a specific port that's not 22
ssh -p 56789 root@localhost
```

```bash
ssh root@127.0.0.1 -p 56789 -N -L 5433:database-url:5432
```

## Double Dash (`--`)
* tells shell to treat any future dashes like strings and not flags
    * `npm test -- -u -t="ColorPicker"`
    * the `-u` is a flag for the command and not `npm`

```bash
grep "--hello" data.txt
grep: unrecognized option '--hello'
```

```bash
grep -- --hello data.txt
```

### Why `git checkout -- file.txt`
* the `--` is optional in this case
* just a good habit, since branches usually have dashes


### sed
`sed -i 's;/resources;~/resources;g' repo.py`

you can use any delimiter char for a sed expression
* doesn’t have to be`/`
* if you know you’re going to have`/`
* you can pick something else to avoid needing to escape `/` a bunch of times

#### [Delete lines that match pattern on mac](https://stackoverflow.com/a/5410784/8479344)
Used in [[work-aws]]
```bash
sed -i '' '/^\[localhost\]:56789/d' ~/.ssh/known_hosts;
```

### How to append to a protected file (with sudo)

```bash
echo '127.0.0.1 redirected-url.com' | sudo tee -a /etc/hosts
```


### Less
- `-N`show line numbers
- `-`


## Secrets

```bash
read -s PGPASSWORD
your_password
export PGPASSWORD
```