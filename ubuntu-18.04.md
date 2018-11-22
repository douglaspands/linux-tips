  # UBUNTU 18.04 LTS
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
  Substituir **errors=remount-ro** por **discard,noatime,errors=remount-ro**.    
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
  ```shell
  sudo add-apt-repository ppa:linrunner/tlp
  sudo apt-get update 
  sudo apt-get install --no-install-recommends tlp tlp-rdw ethtool smartmontools 
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
  ### Resolução 720p
  Em telas com resolução HD, o tamanho da fonte `default` é muito grande.
  Instalando o app `GNOME Tweak Tool`, ele vai permitir mudar o fonte do sistema todo, menos do `Gnome Shell` (Topbar e menu de aplicações).   
  Abaixo estão 2 alternativas para resolver o problema:   
     
  **1. Criar um tema novo**   
  Instale a extensão do Gnome chamado `User Themes` pela loja do Ubuntu.
  Criar um tema e as seguintes pastas e arquivos:
  ```sh
  mkdir -p ~/.themes
  cd ~/.themes
  mkdir -p ubuntu-shell-720p
  cd ubuntu-shell-720p
  mkdir -p gnome-shell
  cd gnome-shell
  gedit gnome-shell.css
  ```
  Editar o arquivo e salvar
  ```css
  @import url("/usr/share/gnome-shell/theme/ubuntu.css");
  stage {
    font-family: Ubuntu, Cantarell, Sans-Serif;
    font-size: 9pt;
  }
  ```
  Após editar o arquivo e salvar, entrar no `Gnome Tweak Tool` na aba `Aparência`.
  No `Tema/Shell` mudar de padrão para `Ubuntu-shell-720p` e fechar o `Gnome Tweal Shell`. Após isso, o `Gnome Shell` estará com o tamanho de fonte alterado.

  **2. Alterar configurações nativas**   
  Para os 2 arquivos abaixo, executar as mesmas alterações:
  1. Substituir `font-size: 10px` para `font-size: 8px`; 
  2. Substituir `font-size: 11px` para `font-size: 9px`; 
  3. Substituir `font-size: 12px` para `font-size: 10px`;
  4. Substituir `font-size: 13px` para `font-size: 11px`;
  5. Substituir `font-size: 14px` para `font-size: 12px`;   
  ```shell
  sudo gedit /usr/share/gnome-shell/theme/gdm3.css
  sudo gedit /usr/share/gnome-shell/theme/gnome-shell.css
  ```
  As demais fontes, alterar pelo app `GNOME Tweak Tool`.
  ### Extensões Gnome
  As extensões Gnome tambem estão disponiveis na loja de aplicativos do Ubuntu (eu aconselho instalar por ela).
  #### No Title Bar
  Remove a barra da janela e inclui os botões de minimar, mazimizar e fechar na barra de status
  #### Status Area Horizontal Spacing
  Remove a distancia dos aplicativos no canto direito da barra de status.
  > Em uso (distancia: 3)
  #### Window Corner Preview
  Permite que fique um PIP da janela de sua escolha em segundo plano. 
  > Em uso (muito util)
  #### User Themes
  Permite criar temas customizados.
  #### Unite
  Deixa a interface do Gnome parecido com a Unity.
