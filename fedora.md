# FEDORA

## Drivers

### Nvidia (mais recente)
```sh
sudo dnf install akmod-nvidia xorg-x11-drv-nvidia-cuda
```
> Adicionar repositorio RPM Fusion antes.


## Customizações e correções

### Montar segundo disco permanentemente no formato NTFS
Antes de começar, garanta que estejam instaladas as libs necessarias:
```sh
sudo dnf install ntfs-3g fuse
```

Capture o UUID do disco que deseja montar com o comando abaixo:
```sh
sudo lsblk -f
```
Vai ser apresentado algo assim:
```sh
NAME        FSTYPE FSVER LABEL  UUID                                 FSAVAIL FSUSE% MOUNTPOINTS
sda                                                                                 
├─sda1                                                                              
└─sda2      ntfs                251729E57BF19D8E                      738,6G    21% /mnt/backup
sdb                                                                                 
├─sdb1      vfat   FAT32        D858-CCAE                             579,5M     3% /boot/efi
├─sdb2      ext4   1.0          70525307-80fa-4466-834f-24b7636c2af0    1,2G    31% /boot
└─sdb3      btrfs        fedora ee79817c-44b0-444d-8197-5e665a8d74db  414,6G     6% /home
                                                                                    /
zram0       swap   1     zram0  234c72bb-fa0f-4269-bd86-6496d1e405d6                [SWAP]
nvme0n1                                                                             
├─nvme0n1p1 vfat   FAT32        3096-DC7D                                           
├─nvme0n1p2                                                                         
├─nvme0n1p3 ntfs                B85698CC56988D2E                                    
└─nvme0n1p4 ntfs                3896986196982204     
``` 
Disco que sera montado é o sda2 com o UUID `251729E57BF19D8E`.
Editar o `/etc/fstab` com sudo usuario:
```sh
sudo nano /etc/fstab
```
Acrescentar uma linha no final com as seguintes infomrmações:
```sh
UUID=251729E57BF19D8E /mnt/backup  ntfs-3g  noacsrules,noatime,nofail,prealloc,sparse  0  0 
```

### Aplicativo nativo da camera (snapshot) não funciona
Incluir no arquivo `~/.bashrc` o seguinte comando:
```sh
export GSK_RENDERER=gl
```

## Aplicações e Utilitarios

### Instalar fontes
Microsoft Core Fontes:
```sh
sudo dnf install curl cabextract xorg-x11-font-utils fontconfig
```
```sh
curl -LO https://downloads.sourceforge.net/project/mscorefonts2/rpms/msttcore-fonts-installer-2.6-1.noarch.rpm
```
```sh
sudo rpm -ivh --nodigest --nofiledigest msttcore-fonts-installer-2.6-1.noarch.rpm
```

Monospace fontes:
```sh
sudo dnf install fira-code-fonts
sudo dnf install cascadia-code-fonts
```

### Instalar VSCode
```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc && echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\nautorefresh=1\ntype=rpm-md\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" | sudo tee /etc/yum.repos.d/vscode.repo > /dev/null
dnf check-update && sudo dnf install code
``` 

### Tema de compatibilidade com o legado
```sh
sudo dnf install adw-gtk3-theme
``` 
> Usar o Gnome-Tweaks para selecionar o tema para os aplicativos legados

## Gnome Plugins

### AppIndicator - Icone no Shell do Gnome (Legado)

Url: [appindicator-support](https://extensions.gnome.org/extension/615/appindicator-support/)

### AlphabeticalAppGrid - Ordenação de apps por ordem alfabetica

URL: [alphabetical-app-grid](https://extensions.gnome.org/extension/4269/alphabetical-app-grid/)
