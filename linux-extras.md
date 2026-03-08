# LINUX EXTRAS

## DISPOSITIVOS

### WiiMote

Para funcionar o controle do Wii no Linux, é necessário dar permissões para ele.
Incluir as seguintes linhas como sudo no arquivo `/etc/udev/rules.d/51-wiimote.rules`:

```sh
#GameCube Controller Adapter
SUBSYSTEM=="usb", ENV{DEVTYPE}=="usb_device", ATTRS{idVendor}=="057e", ATTRS{idProduct}=="0337", TAG+="uaccess"

#Wiimotes or DolphinBar
SUBSYSTEM=="hidraw*", ATTRS{idVendor}=="057e", ATTRS{idProduct}=="0306", TAG+="uaccess"
SUBSYSTEM=="hidraw*", ATTRS{idVendor}=="057e", ATTRS{idProduct}=="0330", TAG+="uaccess"
```

Fonte: https://github.com/dolphin-emu/dolphin/blob/master/Data/51-usb-device.rules
