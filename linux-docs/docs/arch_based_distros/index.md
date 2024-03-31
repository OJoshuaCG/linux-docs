## Instalacion

Esta configuracion de instalacion es util para cualquier distribucion basada en [Arch Linux](https://archlinux.org/), como por ejemplo [Manjaro](https://manjaro.org/), [Archcraft](https://archcraft.io/), [Artix Linux](https://artixlinux.org/), [Garuda Linux](https://garudalinux.org/), [Arco Linux](https://arcolinux.com/), [EndeavourOS](https://endeavouros.com/), entre [otros](https://wiki.archlinux.org/title/Arch-based_distributions_(Espa%C3%B1ol)).

Esta es la tabla de particiones que puede utilizarse en una particion Dualboot

| Tamaño                | Sistema de archivos | Punto de montaje      | Flags |
| --------------------- | ------------------- | --------------------- | ----- |
| 512 MB                | fat32               | /boot/efi o <br>/boot | boot  |
| 4096 MB o <br>2048 MB | linux swap          | -                     | -     |
| ALL                   | ext4                | /                     | -     |

!!! abstract "Dualboot"
    Es una partición del disco de almacenamiento para instalar dos diferentes sistemas operativos.

---
## Post instalacion

Actualizar sistema y activar `base-devel` para instalar paquetes [AUR](http://aur.archlinux.org)

```sh
# Actualizar sistema
sudo pacman -Syyu

# Instalar git y base-devel
pacman -S --needed git base-devel

# Instalar yay con makepkg
mkdir aur
cd aur
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si

# Instalar debtap para instalar paquetes .deb
yay -S debtap
sudo debtap -u
```


---
## Instalacion de paquetes

### Con `pacman`
```sh
sudo pacman -S <PACKAGE_NAME>
```

### Paquete `.tar.xz`
```sh
sudo pacman -U package.pkg.tar.xz
```

### Paquete clonado de AUR o con archivo `PKGBUILD`
```sh
git clone <URL_REPOSITORY>
cd <FOLDER>

# Dentro de la carpeta, debe existir el archivo PKGBUILD
makepkg -si
```

### Con `yay`
```sh
yay -S <PACKAGE_NAME>
```

### Con `debtap`
```sh
sudo debtap <FILENAME>.deb
sudo pacman -U <PACKAGE_NAME>.pkg.tar.zst

# Generando PKGBUILD (opcional)
debtap -P <FILENAME>.deb
```


---

## Desinstalar paquetes

```sh
sudo pacman -R <PACKAGE_NAME>

# Eliminar paquetes y dependencias
sudo pacman -Rn <PACKAGE_NAME>

# Eliminar paquetes, dependencias y demas paquetes que dependen de esas dependencias
sudo pacman -Rsc <PACKAGE_NAME>
```


---

## Busqueda de/en paquetes

Se pueden realizar distintos formatos de busqueda, como por ejemplo

```sh
pacman -Ss <STRING> # (1)
pacman -Ss '^vim-'

# Buscar paquetes instalados
pacman -Qs <PACKAGE_NAME>

# Conocer informacion de un paquete
pacman -Si <PACKAGE_NAME>

# Conocer informacion de un paquete instalado
pacman -Qi <PACKAGE_NAME>

# Obtener lista de los archivos instalados por un paquete
pacman -Ql <PACKAGE_NAME>

# Buscar un paquete que contenga un archivo
pacman -Fy # (2)
pacman -Fs <FILENAME>
```

1. Tomar en cuenta que la busqueda es de tipo `regex`
2. Actualizar base de datos


---
## Comandos utiles para pacman

```sh
# Listar paquetes instalados
pacman -Qe

# Quitar dependencias innecesarias
sudo pacman -Rs $(pacman -Qdtq)

# Limpiar cache del sistema de paquetes
sudo pacman -Scc
```


---
## Evitar actualizacion de paquetes

```sh
sudo nano /etc/pacman.conf

  IgnorePkg = linux mariadb mysql postgresql python2 franz beekeeper-studio
```