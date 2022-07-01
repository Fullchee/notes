```bash
docker exec -it $(docker ps --filter name=$1 -q) ${2:-bash}
```

`ce app`
