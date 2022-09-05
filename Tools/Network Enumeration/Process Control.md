# PS
Show all process running on system, greppable

```bash
ps aux | grep 646
```

Kill the process
```bash
sudo kill -9 646
```

# lsof - list open files
```bash
lsof -n -i4TCP:80
```
