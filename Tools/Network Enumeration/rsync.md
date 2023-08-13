Connect to remote file-copying tool

### Usage
List shares with no password on port 873
```shell
rsync --list-only 10.129.228.37::
```

List files in share `public`
```shell
rsync --list-only 10.129.228.37::public
```

Copy flag to our machine
```shell
rsync 10.129.228.37::public/flag.txt flag.txt
```
