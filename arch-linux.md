# ARCH LINUX

## pacman

### upgrade
```sh
sudo pacman -Syu --noconfirm
```

### autoremove
```sh
sudo pacman -Rs $(pacman -Qtdq) 
```

### clear cache
```sh
sudo pacman -Sc --noconfirm
```

## yay

### upgrade
```sh
yay -Syu --noconfirm
```

### autoremove
```sh
yay -Rs $(yay -Qtdq) 
```

### clear cache
```sh
yay -Sc --noconfirm
```

## KDE

### Usar o Dolphin com o root
```sh
sudo pacman -S --noconfirm --needed kio-admin 
```
`alt + ctrl + shift + a` para abrir no modo root.
> Apesar de ajudar, facilita o uso do super usuario, o que não é recomendado.

### Montar `.iso` no Dolphin
```sh
sudo pacman -S --noconfirm --needed kio-fuse kio-extras
```
Clicar com o botão direito do mouse no `*.iso` e clicar em `montar`.

## systemd-boot

### Listar kernels do boot
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

### Escolher o kernel default no boot
```sh
sudo bootctl set-default 2025-08-27_04-38-50_linux-zen.conf
```
> `2025-08-27_04-38-50_linux-zen.conf` id do kernel escolhido

## Aplicações
Apoio a instalação de aplicações essenciais (na minha opinião).

### Build essentials
```sh
sudo pacman -Sy --noconfirm --needed base-devel git curl less openssl zlib xz tk zstd
```

### Docker + Compose
```sh
sudo pacman -Sy --noconfirm --needed docker docker-compose
```
Adicionar usuario ao grupo do Docker:
```sh
sudo usermod -aG docker $USER
```

### Nvidia Container Toolkit
```sh
sudo pacman -Sy --noconfirm --needed nvidia-container-toolkit
```
Configurar o Docker daemon:
```sh
sudo nvidia-ctk runtime configure --runtime=docker && \
sudo systemctl restart docker
```

### Terminator
```sh
sudo pacman -Sy --noconfirm --needed terminator
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

### Opera (AUR)
```sh
yay -S --noconfirm --quiet --needed opera
```
> O **Opera** é o unico navegador que roda videos em fullhd no Netflix.  

> Caso ocorra problemas para assistir videos nos streamings, o repositorio [fix-opera-linux-ffmpeg-widevine](https://github.com/Ld-Hagen/fix-opera-linux-ffmpeg-widevine) tem uma dica valiosa para destravar.
