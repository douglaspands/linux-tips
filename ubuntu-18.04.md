# UBUNTU 18.04 LTS
___
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
## SWAP
### Swappiness
Reduzir o consumo de memoria `swap` (memoria em disco) 
```shell
echo -e "vm.swappiness=10" | sudo tee -a /etc/sysctl.conf
echo -e "vm.vfs_cache_pressure=50" | sudo tee -a /etc/sysctl.conf
```
### Preload
Aplicativo que ajuda a aumentar a agilidade da abertura de programas que geralmente você usa diariamente, navegadores, editores de texto ou players de som.
Ele se mantém rodando em background, sem solicitar nenhuma intervenção do usuário, monitorando quais são os programas mais utilizados, movendo-os para áreas mais acessíveis do disco, ou mesmo pré-carregando algumas partes de programas mais complexos e muito utilizados, dando um perceptível ganho em velocidade de uso.
```shell
sudo apt-get install preload
```
## SSD
### Remover auditoria de leitura e adicionar trim
```shell
sudo gedit /etc/fstab
```
Substituir **errors=remount-ro** por **discard,nodiratime,noatime,errors=remount-ro**.    
Salvar e reiniciar o computador.
## NVIDIA GPU
### Instalar nvidia-driver-415 (mais atual)
```shell
sudo apt-get purge nvidia*
sudo add-apt-repository ppa:graphics-drivers
sudo apt-get update
sudo apt install nvidia-driver-415
```
> O driver mais atual é o nvidia-driver-415
### Alternar entre GPU Nvidia e Intel (prime-select)
Usar GPU Intel:
```shell
sudo prime-select intel
```
Usar GPU Nvidia:
```shell
sudo prime-select nvidia
```
Para verificar qual GPU esta ativa
```shell
prime-select query
```
### Remover tearing
Fonte: [Diolinux](https://www.diolinux.com.br/2018/07/como-resolver-o-problema-de-screen.html)
```shell
echo -e "options nvidia-drm modeset=1" | sudo tee -a /etc/modprobe.d/nvidia-drm-nomodeset.conf
sudo update-initramfs -u
sudo reboot
```
Após iniciar, consulte se deu certo:
```shell
sudo cat /sys/module/nvidia_drm/parameters/modeset
```
Tem que aparecer um "Y".
  
## LAPTOP
### TLP - Economizar bateria
Ferramenta em linha de comando para gerenciamento de energia.
```shell
sudo add-apt-repository ppa:linrunner/tlp
sudo apt-get update 
sudo apt-get install --no-install-recommends tlp tlp-rdw ethtool smartmontools 
```
### TLPUI - Inteface Visual
Interface visual da ferramenta TLP para gerenciamento de energia.
```shell
sudo add-apt-repository ppa:linuxuprising/apps
sudo apt update
sudo apt install tlpui
```
## MEMORIAS (RAM, CACHE, ETC...)
### Verificar a RAM e slots disponiveis
```shell
sudo dmidecode --type 17
```
No resultado, tem 3 informações importantes: `Type`, `Speed` e `Size`.
```shell
# dmidecode 3.1
Getting SMBIOS data from sysfs.
SMBIOS 2.8 present.
  
Handle 0x0011, DMI type 17, 34 bytes
Memory Device
  Array Handle: 0x0010
  Error Information Handle: No Error
  Total Width: 64 bits
  Data Width: 64 bits
  Size: 8192 MB
  Form Factor: SODIMM
  Set: None
  Locator: ChannelA-DIMM0
  Bank Locator: BANK 0
  Type: DDR3
  Type Detail: Synchronous
  Speed: 1600 MT/s
  Manufacturer: 0715
  Serial Number: 00191924
  Asset Tag: 9876543210
  Part Number: TMT41GS6BFR8A-PBHJ
  Rank: 2
  Configured Clock Speed: 1600 MT/s
  
Handle 0x0012, DMI type 17, 34 bytes
Memory Device
  Array Handle: 0x0010
  Error Information Handle: No Error
  Total Width: Unknown
  Data Width: Unknown
  Size: No Module Installed
  Form Factor: DIMM
  Set: None
  Locator: ChannelB-DIMM0
  Bank Locator: BANK 2
  Type: Unknown
  Type Detail: None
  Speed: Unknown
  Manufacturer: Not Specified
  Serial Number: Not Specified
  Asset Tag: 9876543210
  Part Number: Not Specified
  Rank: Unknown
  Configured Clock Speed: Unknown
```
### Verificar a RAM e as demais memorias
```shell
sudo lshw -short -C memory
```
O relatorio será assim:
```shell
Caminho do hardware  Dispositivo  Classe         Descrição
============================================================
/0/0                              memory         128KiB BIOS
/0/4/8                            memory         32KiB L1 cache
/0/4/9                            memory         256KiB L2 cache
/0/4/a                            memory         3MiB L3 cache
/0/7                              memory         32KiB L1 cache
/0/10                             memory         8GiB Memória do sistema
/0/10/0                           memory         8GiB SODIMM DDR3 Síncrono 1600 MHz (0,6 ns)
/0/10/1                           memory         DIMMProject-Id-Version: lshwReport-Msgid-Bugs-To: FULL NAME <EMAIL@ADDRESS>PO-Revision-Date: 2013-04-07 17:30+0000Last-Translator: Neliton
```
## GNOME
### Touchpad (tap-to-click) no GDM (Tela de Login)
```shell
sudo -i
xhost +SI:localuser:gdm
su gdm -s /bin/bash
gsettings set org.gnome.desktop.peripherals.touchpad tap-to-click true
sudo reboot
```
Se quiser voltar atrás, execute todos os comandos anteriores, porem, no passo 4, execute o comando abaixo:
```shell
gsettings set org.gnome.desktop.peripherals.touchpad tap-to-click false
```
### Monitor com resolução 720p (1366x768)
Para monitores com resolução 720p (1366x768) o tamanho da fonte padrão é muito grande.
Para corrigir isso, é necessario editar o mesmo ponto nos seguintes arquivos:
```shell
sudo gedit /usr/share/gnome-shell/theme/gdm3.css
sudo gedit /usr/share/gnome-shell/theme/gnome-shell.css
sudo gedit /usr/share/gnome-shell/theme/ubuntu.css
```
Alterar o tamanho do fonte global de `11pt` para `9pt` (costuma ficar no inicio do codigo):
```css
/* GLOBALS */
stage {
  font-family: Cantarell, Sans-Serif;
  font-size: 9pt; /* <== Substituir de 11pt para 9pt */ 
  color: #eeeeec; }
```
As demais fontes, alterar pelo app `GNOME Tweak Tool`.

### Extensões Gnome
#### No Title Bar
Remove a barra da janela e inclui os botões de minimar, mazimizar e fechar na barra de status
#### Status Area Horizontal Spacing
Remove a distancia dos aplicativos no canto direito da barra de status.
> Em uso (distancia: 1)
#### Window Corner Preview
Permite que fique um PIP da janela de sua escolha em segundo plano. 
![screenshot_1227.png](https://extensions.gnome.org/extension-data/screenshots/screenshot_1227.png)
> Em uso (muito util)   
#### User Themes
Permite criar temas customizados.
#### Unite
Deixa a interface do Gnome parecido com a Unity.
  
