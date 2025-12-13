# FEDORA

## Drivers

### Nvidia (mais recente)
```sh
sudo dnf install akmod-nvidia xorg-x11-drv-nvidia-cuda
```
> Adicionar repositorio RPM Fusion antes.

## Aplicações e Utilitarios

### Instalar fontes
```sh
sudo dnf install mscore-fonts-all
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
