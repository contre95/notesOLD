
### Memory and CPU usage of all containers

```bash
docker ps -q | xargs  docker stats --no-stream
```
