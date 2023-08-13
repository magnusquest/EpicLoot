Database

### Connect
Use `psql` command
```shell
psql -U christine -h localhost -p 1234
```

Use `\l` to list databases, `\c` to cd, and `\dt` to show relations

Execute PSQL queries as follows:
```psql
select * from flag;
```