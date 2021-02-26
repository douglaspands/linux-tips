# LINUX MINT 

## VERIFICAR HARDWARE
```shell
inxi -Fxz
```
## SOFTWARE
### Desinstalar aplicativo sem remover dependencias
```shell
dpkg -r --force-depends foo
```
Remove aplicativo, mas não remove suas configurações e nem o \*.deb do cache
```shell
dpkg -P --force-depends foo
```
Remove aplicativo (inclusive do cache) e suas configurações.
### Verificação de dependencias reversas
Será verificado todos os apps que dependem desse pacote.
```shell
apt-cache rdepends packagename
```
### Remover pacotes orfãos
```shell
sudo apt install gtkorphan
```
Via interface visual, é listado todos os pacotes orfãos podendo ser removidos apenas ticando a aplicação e clicando no botão OK. 
### SNAP - Remover pacotes velhos (que já foram atualizados e estão desabilitados)
Criar arquivo `shellscript` com o nome `snap_remove_old.sh` com o seguinte conteudo:
```sh
#!/bin/bash
# Removes old revisions of snaps
# CLOSE ALL SNAPS BEFORE RUNNING THIS
set -eu
snap list --all | awk '/disabled/{print $1, $3}' |
    while read snapname revision; do
        snap remove "$snapname" --revision="$revision"
    done
```
Depois executar esse arquivo como `sudo`:
```sh
sudo sh snap_remove_old.sh
```
### SNAP - Acesso a outros discos / pendrive / sd
Darei acesso a outros discos e medias para a aplicação `retroarch` no formato `snap` (exemplo):
```shell
sudo snap connect retroarch:removable-media
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

### PRELOAD
Aplicativo que ajuda a aumentar a agilidade da abertura de programas que geralmente você usa diariamente, navegadores, editores de texto ou players de som.
Ele se mantém rodando em background, sem solicitar nenhuma intervenção do usuário, monitorando quais são os programas mais utilizados, movendo-os para áreas mais acessíveis do disco, ou mesmo pré-carregando algumas partes de programas mais complexos e muito utilizados, dando um perceptível ganho em velocidade de uso.
```shell
sudo apt-get install preload
```

## HYBRID GPU DRIVER
### INSTALAR DRIVER NVIDIA 920M (VERSAO 430)
```shell
sudo apt-get purge *nvidia*
sudo rm /lib/modprobe.d/blacklist-nvidia.conf
sudo apt-get update
sudo apt-get --install-recommends install nvidia-driver-430 nvidia-prime-applet 
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

## Bluetooth Driver (Acer E5-573G)
Adicionar as seguintes linhas no arquivo `etc/modprobe.d/btconfig.conf`:
```bash
blacklist acer_wmi
options ath9k btcoex_enable=1 bt_ant_diversity=1
```
> O Wifi e o Bluetooth é fornecido pelo mesmo componente `Qualcomm Atheros QCA9565 / AR9565 Wireless Network Adapter`. 

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
## SNAP
### UPDATE ALL
```shell
sudo snap refresh
```

## FLATPAK
### UPDATE ALL
```shell
flatpak update
```
## INTERFACE
### QT LIKE GTK
Entrar nas configurações
```shell
qt5ct
```
dica: [Temas GTK em aplicações Qt](https://www.diolinux.com.br/2019/02/temas-gtk-em-aplicacoes-qt.html)
