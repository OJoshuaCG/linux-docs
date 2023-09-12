## Crear usuario



## Montar particiones automaticamente al iniciar sesion

Si tenemos windows:

1. Desactivar la opcion `Activar inicio rapido` dentro del panel de control:
2. **Panel de control\Todos los elementos de Panel de control\Opciones de energía\Configuración del sistema** seleccionamos `Cambiar la configuracion no disponible actualmente` y desactivar la opcion `Activar inicio rapido`, guardamos los cambios.

En Linux,

1. Instalar el paquete `ntfs-3g` en nuestro sistema.
2. Ejecutar el comando `lsblk -f` para mostrar las particiones y copiar el codigo **UUID**.

```bash
sudo pacman -S ntfs-3g

lsblk -f
    # OUTPUT
    NAME   FSTYPE FSVER LABEL    UUID                                 MOUNTPOINTS
    sda
    ├─sda1 vfat   FAT32          528F-2C22
    ├─sda2
    ├─sda3 ntfs                  1E7A98767A984C81
    ├─sda4 ntfs                  BA6288AA62886CC7
    ├─sda5 ntfs         Data     1CBEAA97BEAA68CA                      /run/media/user/Data
    ├─sda6 vfat   FAT32 NO_LABEL 5BE5-6C43                             /boot/efi
    ├─sda7 swap   1              10bbf2a7-7d2f-4d8c-8198-b4185dfbad82  [SWAP]
    └─sda8 ext4   1.0            cf3e6ce0-43c7-4764-b0f1-91b7454595be  /
```

!!! info "Ayuda"
    Si queremos, por ejemplo, la particion `sda5` con el `UUID = 1CBEAA97BEAA68CA`, el cual tiene el formato (_FSTYPE_) `ntfs`;
    es necesario montar estas unidades en la ubicacion `/mnt` agregando el nombre de la carpeta con la que que localizaremos la particion, en nuestro caso es `Data`, de esta forma todos los archivos se ubicaran en `/mnt/Data`.

3. Abrir el archivo `/etc/fstab` y agregaremos la siguiente linea

```bash
sudo nano /etc/fstab

# Linea a agregar
UUID=1CBEAA97BEAA68CA /mnt/Data ntfs defaults 0 0

# Nomenclatura (NO agregar)
UUID=UUID_PARTICION PUNTO_A_MONTAR TIPO_FORMATO defaults 0 0
```

Estos cambios se guardan y se veran reflejados despues de reinicar el equipo. En algunos casos en lugar de establecer el formato "ntfs", se cambia a "ntfs-3g"


---
## Como instalar fuentes en linux

Para instalar fuentes, debemos descargarlas primero y simplemente moverlas como usuario `root` al directorio `/usr/share/fonts/`

A continuacion se comparte un enlace para descargar unas fuentes, simplemente hay que ejecutar los siguientes comandos:

```bash
sudo su
cd /usr/share/fonts/
wget "https://onedrive.live.com/download?cid=9BA28230294BA989&resid=9BA28230294BA989%21835&authkey=AJ2I8HETi5LMlxk"
# or
wget "https://onedrive.live.com/download.aspx?authkey=%21AAy55dITXmJA6r4&resid=9BA28230294BA989%21864&cid=9BA28230294BA989&parId=root&parQt=sharedby&o=OneUp"

# rename the file with 'mv' cmd
mv "downloaded_file" pf.zip
unzip pf.zip
rm pf.zip
```

_Fuentes incluidas:_

- azuki
- Cartograph CF
- Cascadia Code
- Fira Code
- Hack Nerd Font
- icomoon
- iosevka
- JetBrains Mono
- Lilex
- Material Icons
- Roboto


---
## Habilitar camara externa

```sh
sudo pacman -S v4l2-ctl cameractrls

v4l2-ctl --list-devices
v4l2-ctl -d /dev/video0 --list-ctrls

# Open cameractrls and search:  "Real Path" from "Capture"
# Copy and do this:
sudo mv /dev/video0 /dev/video0.original
sudo mv /dev/video2 /dev/video0

# - Where /dev/video2 is "Real Path" from external camera

# For revert actions:
sudo mv /dev/video0 /dev/video2
sudo mv /dev/video0.original /dev/video0
```


---
## Internet

```bash
sudo pacman -S linux-firmware networkmanager wpa_supplicant netctl wireless_tools dialog dhcpcd broadcom-wl broadcom-wl-dkms iwlwifi


# Verificar driver
lspci | grep Wireless
lspci -k

ip link
ip link set <interface> up

# Example
ip link set wlan0 up
ip link set wlp2s0 up
ip link set enp3s0 up

rfkill
rfkill unblock wifi
```
