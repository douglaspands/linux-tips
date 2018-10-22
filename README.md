# LINUX MINT 19 

## VERIFICAR HARDWARE
```shell
inxi -Fxz
```

## SSD
### SWAPINESS
```shell
echo -e "vm.swappiness=10" | sudo tee -a /etc/sysctl.conf
echo -e "vm.vfs_cache_pressure=50" | sudo tee -a /etc/sysctl.conf
```
### REMOVER AUDITORIA DE LEITURA E ADICIONAR TRIM 
```shell
sudo xed /etc/fstab
```
Now change “errors=remount-ro” to “discard,noatime,errors=remount-ro”.    
Save the file and reboot.

## HYBRID GPU DRIVER
### INSTALL NVIDIA DRIVER ONLY (396)
```shell
sudo apt-get purge nvidia*
sudo add-apt-repository ppa:graphics-drivers
sudo apt-get update
sudo ubuntu-drivers autoinstall
```
### REMOVE TEARING (NVIDIA)
Fonte: [Diolinux](https://www.diolinux.com.br/2018/07/como-resolver-o-problema-de-screen.html)
```shell
sudo gedit /etc/modprobe.d/nvidia-drm-nomodeset.conf
```
digite e depois salve: 
```txt
options nvidia-drm modeset=1
```
Execute no shell:
```shell
sudo update-initramfs -u
sudo reboot
```
Após iniciar, consulte se deu certo:
```shell
sudo cat /sys/module/nvidia_drm/parameters/modeset
```
Tem que aparecer um "Y".

### NVIDIA PRIME: CHANGE BETWEEN NVIDIA AND INTEL (TERMINAL)
Use Intel GPU:
```shell
sudo prime-select intel
```
Use Nvidia GPU:
```shell
sudo prime-select nvidia
```
### PROBLEMA NO SOM APÓS ATUALIZAÇÃO DO DRIVER
Após a atualização do driver de video, o Linux Mint começou a direcionar o audio para o HDMI, mas a central de som do Mint não identificava isso. Para resolver, foi necessario instalar o app **pavucontrol**.
```shell
sudo apt-get install pavucontrol
pavucontrol
```
Ao acessar, mudar a saida de audio do HDMI. Ao mudar, ele indetificará que não esta plugado e resolverá o problema.

## BATTERY SAVE (LAPTOP)
### INSTALL TLP – Linux Advanced Power Management
Fonte: [Blog do Edivaldo](https://www.edivaldobrito.com.br/tlp-no-ubuntu/)   
Fonte: [TLP](https://linrunner.de/en/tlp/tlp.html)   
```shell
sudo apt-get purge laptop-mode-tools
sudo add-apt-repository ppa:linrunner/tlp
sudo apt-get update
sudo apt-get install tlp tlp-rdw
sudo tlp start
```
## REMOVER PACOTE SEM REMOVER AS DEPENDENCIAS
```shell
dpkg -P --force-depends foo
```
