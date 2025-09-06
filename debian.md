# DEBIAN

## Instalar driver da Nvidia (mais recente)
Instalar as seguintes dependencias:
```sh
sudo apt install -y linux-headers-amd64 build-essential
```
Download: [Nvidia Drivers](https://www.nvidia.com/en-in/drivers/)   
`NVIDIA-Linux-x86_64-580.82.07.run` é o driver mais recente.

Assim que o download estiver concluido, executar os comandos:
```sh
chmod +x NVIDIA-Linux-x86_64-580.82.07.run
sudo ./NVIDIA-Linux-x86_64-580.82.07.run
```
Vai ser solicitado algumas confirmações, elas variam de acordo com a versão, geramente o sugerido já atende (menos o `Abort Installation`).

Editar o arquivo `/etc/default/grub` com o sudo e acrescentar o parametro `nvidia-drm.modeset=1`
na variavel `GRUB_CMDLINE_LINUX`:
```txt
GRUB_CMDLINE_LINUX="nvidia-drm.modeset=1"
```
> Se já existir algum conteudo nessa variavel, dar um espaço e adicione na frente.
Exemplo: `GRUB_CMDLINE_LINUX="quiet nvidia-drm.modeset=1"`

Feito isso, executar o comando:
```sh
sudo update-grub
```
Após o termino, reiniciar a maquina.


## Opera - Correção HTML5 medias
O navegador Opera (na data 04/09/2025) é o unico navegador que permite assistir videos em FullHD do 
Netflix no Linux. Porem, pode acontecer de dar erro no momento da inicialização do video.
Para corrigir, existe um tutorial no repositorio [fix-opera-linux-ffmpeg-widevine](https://github.com/Ld-Hagen/fix-opera-linux-ffmpeg-widevine) onde contem o passo a passo necessario.


## Davinci Resolve
Instale as seguintes dependencias:
```sh
sudo apt install libapr1 libaprutil1 libasound2 libglib2.0-0
```
> Se alguma falhar, não tem problema, pois essas dependencias são requisitos da aplicação.

Faça o download em: [BlackMagicDesign](https://www.blackmagicdesign.com/br/products/davinciresolve) e instale assim:

```sh
unzip ./DaVinci_Resolve_20.1.1_Linux.zip
chmod +x ./DaVinci_Resolve_20.1.1_Linux.run
sudo SKIP_PACKAGE_CHECK=1 ./DaVinci_Resolve_20.1.1_Linux.run -i
```
Vai solicitar algumas ações, mas é do tipo `Next`, `next`....

Assim que instalado, é necessario mover algumas libs do `Resolve` para funcionar:
```sh
cd /opt/resolve/libs
sudo mkdir disabled-libraries
sudo mv libglib* disabled-libraries
sudo mv libgio* disabled-libraries
sudo mv libgmodule* disabled-libraries
```

Feito isso, a aplicação vai funcionar corretamente.
