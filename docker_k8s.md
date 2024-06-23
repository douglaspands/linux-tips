# Dicas de Docker/K8S

## Remover todos os containers

1. Parar os containers

```bash
docker stop $(docker ps -a -q)
```

2. Remover os containers

```bash
docker rm $(docker ps -a -q)
```

## Adicionar autocomplete do MicroK8s no ZSH
```sh
alias kubectl="microk8s.kubectl"
# use autocompletion
autoload -Uz compinit
compinit

# https://kubernetes.io/docs/tasks/tools/included/optional-kubectl-configs-zsh/
source <(kubectl completion zsh)
alias k=kubectl
compdef k=kubectl

# for microk8s kubectl
microk8s.kubectl() {
    microk8s kubectl "$@"
}
alias mk="microk8s.kubectl"
compdef microk8s.kubectl=kubectl
compdef mk=kubectl
```
