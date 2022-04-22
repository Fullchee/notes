## https://jvns.ca/blog/2022/04/12/a-list-of-new-ish--command-line-tools/

https://explainshell.com/explain?cmd=%s
`tldr`

https://bash3boilerplate.sh/

- has best practices

## Remote machines

### SSH

Create an ssh tunnel
```bash
# ssh to a specific port that's not 22
ssh -p 56789 root@localhost
```

```bash
ssh root@127.0.0.1 -p 56789 -N -L 5433:database-url:5432
```

### Transfer files with [croc](https://github.com/schollz/croc)
```bash
# Terminal 1
$ croc send test.tif
Code is anita-price-quick
```

```bash
# Terminal 2
crock anita-price-quick
```

### tmux: Close a shell without killing the app that it's running

- used at IBM when I connected to the Fyre VM
- an IDE or a long running script

1. `ctrl z` (to send program to background)
2. `disown -a`

## General Tips

### Double Dash (`--`)

- tells shell to treat any future dashes like strings and not flags
  - `npm test -- -u -t="ColorPicker"`
  - the `-u` is a flag for the command and not `npm`

```bash
grep "--hello" data.txt
grep: unrecognized option '--hello'
```

```bash
grep -- --hello data.txt
```

#### Why `git checkout -- file.txt`

- the `--` is optional in this case
- just a good habit, since branches usually have dashes


### Command substitution

```bash
result=$(curl -X GET 'URL')
```

### String substitution

```bash
${var}

"$var_name"
```

## Editing Files
#### [Delete lines that match pattern](https://stackoverflow.com/a/5410784/8479344)

Used in [[work-aws]]

```bash
sed -i '' '/^\[localhost\]:56789/d' ~/.ssh/known_hosts;
```

### How to append to a protected file (with sudo)

```bash
echo '127.0.0.1 redirected-url.com' | sudo tee -a /etc/hosts
```

## Listening to files

### [Entr](https://github.com/eradman/entr)
Run arbitrary commands when files change

### pbcopy & pbpaste

https://osxdaily.com/2007/03/05/manipulating-the-clipboard-from-the-command-line/

* `pbcopy < file.txt`
* `ps aux | pbcopy`


* `pbpaste > pastetest.txt`
* `pbpaste | grep rcp`


### Less

- `-N`show line numbers
- `bat` if possible
    - has syntax highlighting

## Secrets

```bash
read -s PGPASSWORD
secretly_type_your_password
export PGPASSWORD
```

### [direnv](https://github.com/direnv/direnv)
- Checks for `.envrc` > `.env`
- makes them environment variables

## Search

### ripgrep (rg)

* better than `grep`
* [ripgrepall](https://github.com/phiresky/ripgrep-all) also searches PDFs and other files
    * `brew install rga`
    * `brew install pandoc poppler tesseract ffmpeg`


### Read logs

`lnav` has syntax highlighting for logs

### [Hyperfine](https://github.com/sharkdp/hyperfine) CLI Benchmarking Performance


## Typos
- zsh auto recommends a command if you mistype
- for subcommands, use [thefuck](https://github.com/nvbn/thefuck)
    - video: https://user-images.githubusercontent.com/11246258/163878799-c9b01191-e253-4a9b-9818-429d1bc7a30e.mp4