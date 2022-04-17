# sed

## sd
* Alternative to sed
* https://github.com/chmln/sd

* Replace newlines with commas:
    * sd: `sd '\n' ','`
    * sed: `sed ':a;N;$!ba;s/\n/,/g'`


### sed

`sed -i 's;/resources;~/resources;g' repo.py`

you can use any delimiter char for a sed expression

- doesn’t have to be`/`
- if you know you’re going to have`/`
- you can pick something else to avoid needing to escape `/` a bunch of times

### One liner to remove lines that match a pattern from a file

This example removes `[localhost]:56789` from `~/.ssh/known_hosts`

```
sed -i '' '/^\[localhost\]:56789/d' ~/.ssh/known_hosts
```

#### As an alias

```
alias rm-known-localhost="sed -i '' '/^\[localhost\]:56789/d' ~/.ssh/known_hosts"
```

A line in `~/.ssh/known_hosts` looks like

```
[localhost]:56789 name key
```