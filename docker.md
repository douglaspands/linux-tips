# Dicas de Docker

## Remover containers sem uso

1. Para os containers

```bash
docker stop $(docker ps -a -q)
```

2. Remover os containers

```bash
docker rm $(docker ps -a -q)
```
