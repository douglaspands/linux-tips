# ARCH LINUX

## Comandos de apoio

### pacman

#### Upgrade
```sh
sudo pacman -Syu
```

#### Autoremove
```sh
sudo pacman -Rs $(pacman -Qtdq) 
```

#### Clear cache
```sh
sudo pacman -Sc
```

### yay

#### Upgrade
```sh
yay -Syu
```

#### Autoremove
```sh
yay -Rs $(yay -Qtdq) 
```

#### Clear cache
```sh
yay -Sc
```

### systemd-boot

#### Listar kernels do boot
```sh
bootctl list 
```
Ouput:
```txt
         type: Boot Loader Specification Type #1 (.conf)
        title: Arch Linux (linux)
           id: 2025-08-27_04-38-50_linux.conf
       source: /boot//loader/entries/2025-08-27_04-38-50_linux.conf (on the EFI>
        linux: /boot//vmlinuz-linux
       initrd: /boot//initramfs-linux.img
      options: root=PARTUUID=26d26d66-c86e-4be0-b8c2-a0130f00273c zswap.enabled>

         type: Boot Loader Specification Type #1 (.conf)
        title: Arch Linux (linux-zen) (default) (selected)
           id: 2025-08-27_04-38-50_linux-zen.conf
       source: /boot//loader/entries/2025-08-27_04-38-50_linux-zen.conf (on the>
        linux: /boot//vmlinuz-linux-zen
       initrd: /boot//initramfs-linux-zen.img
      options: root=PARTUUID=26d26d66-c86e-4be0-b8c2-a0130f00273c zswap.enabled>

         type: Boot Loader Specification Type #1 (.conf)
```

#### Escolher o kernel default no boot
```sh
sudo bootctl set-default 2025-08-27_04-38-50_linux-zen.conf
```
> `2025-08-27_04-38-50_linux-zen.conf` id do kernel escolhido

## Aplicações

### Build essentials
```sh
sudo pacman -Sy base-devel git curl less
```

### Docker + Compose
```sh
sudo pacman -Sy docker docker-compose
```
Adicionar usuario ao grupo do Docker:
```sh
sudo usermod -aG docker $USER
```

### Nvidia Container Toolkit
```sh
sudo pacman -Sy nvidia-container-toolkit
```
Configurar o Docker daemon:
```sh
sudo nvidia-ctk runtime configure --runtime=docker && \
sudo systemctl restart docker
```

### Terminator
```sh
sudo pacman -Sy terminator
```

### Yay - Gerenciador de repositorios AUR
```sh
git clone https://aur.archlinux.org/yay-bin.git && cd yay-bin && makepkg -si
```

### Fontes da Microsoft (AUR)
```sh
yay -S --noconfirm --quiet --needed ttf-ms-fonts
```

### Google Chrome (AUR)
```sh
yay -S --noconfirm --quiet --needed google-chrome
```

### Visual Studio Code (AUR)
```sh
yay -S --noconfirm --quiet --needed visual-studio-code-bin
```
