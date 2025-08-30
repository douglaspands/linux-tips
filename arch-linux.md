# ARCH LINUX

## AUR - Arch User Repository

### Yay - Gerenciador de repositorios AUR
```sh
git clone https://aur.archlinux.org/yay-bin.git && cd yay-bin && makepkg -si
```

### Comandos

#### Clear cache
```sh
yay -Sc
```

#### Autoremove
```sh
yay -Rs $(yay -Qtdq) 
```

### Repositorios

#### Fontes da Microsoft
```sh
yay -S --noconfirm --quiet --needed ttf-ms-fonts
```

#### Google Chrome
```sh
yay -S --noconfirm --quiet --needed google-chrome
```

#### Visual Studio Code
```sh
yay -S --noconfirm --quiet --needed visual-studio-code-bin
```

## Pacman

### Comandos

#### Autoremove
```sh
sudo pacman -Rs $(pacman -Qtdq) 
```

### Aplicações

#### Build essentials
```sh
sudo pacman -Sy base-devel git curl less
```

#### Docker + Compose
```sh
sudo pacman -Sy docker docker-compose
```
Adicionar usuario ao grupo do Docker:
```sh
sudo usermod -aG docker $USER
```

#### Nvidia Container Toolkit
```sh
sudo pacman -Sy nvidia-container-toolkit
```
Configurar o Docker daemon:
```sh
sudo nvidia-ctk runtime configure --runtime=docker && \
sudo systemctl restart docker
```

#### Terminator
```sh
sudo pacman -Sy terminator
```
