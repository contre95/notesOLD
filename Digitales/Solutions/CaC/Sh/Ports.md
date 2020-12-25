# Check open ports

With **Netstats**

```sh
 netstat -ltnp | grep -w ':80' 
```

- `l` – tells netstat to only show listening sockets.
- `t` – tells it to display tcp connections.
- `n` – instructs it show numerical addresses.
- `p` – enables showing of the process ID and the process name.
- `grep -w` – shows matching of exact string (:80).

With **lsof**

```shell
lsof -i :80
```
