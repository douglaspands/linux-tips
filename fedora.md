# FEDORA

## Drivers

### Nvidia (mais recente)
```sh
sudo dnf install akmod-nvidia xorg-x11-drv-nvidia-cuda
```
> Adicionar repositorio RPM Fusion antes.

### Intel + Nvidia Optimus

> Especificado em cima da minha placa Nvidia 920M


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
