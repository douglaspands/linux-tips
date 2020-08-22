# Dicas de Docker

## Remover todos os containers

1. Parar os containers

```bash
docker stop $(docker ps -a -q)
```

2. Remover os containers

```bash
docker rm $(docker ps -a -q)
```
