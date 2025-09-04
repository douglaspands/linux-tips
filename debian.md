# DEBIAN

## Instalar driver da Nvidia
Download: [Nvidia Drivers](https://www.nvidia.com/en-in/drivers/)   
`NVIDIA-Linux-x86_64-580.82.07.run` é o driver mais recente.

Instalar as seguintes dependencias:
```sh
sudo apt install -y linux-headers-amd64 build-essential
```

Editar o arquivo `/etc/modprobe.d/supergfxd.conf` com sudo:
```txt
blacklist nouveau
alias nouveau off

option nvidia-drm modeset=1
```

Assim que o download estiver concluido, executar os comandos como no exemplo abaixo:
```sh
chmod +x NVIDIA-Linux-x86_64-580.82.07.run
sudo ./NVIDIA-Linux-x86_64-580.82.07.run
```
