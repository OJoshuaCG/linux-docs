_Esta documentacion esta realizada en base a Open Suse Leap 15.5_

## Post instalacion

Actualizar el sistema:

```sh
sudo zypper ref && sudo zypper up
zypper update

zypper install sudo wget curl
```

Agregar el gestor de paquetes `packman`

_**Solo paquetes esenciales:**_

```sh
zypper ar -cfp 90 'https://ftp.gwdg.de/pub/linux/misc/packman/suse/openSUSE_Leap_$releasever/Essentials' packman-essentials

zypper dup --from packman-essentials --allow-vendor-change
```

_**Todos los paquetes:**_

```sh
zypper ar -cfp 90 'https://ftp.gwdg.de/pub/linux/misc/packman/suse/openSUSE_Leap_$releasever/' packman

zypper dup --from packman --allow-vendor-change
```

Refrescamos las llaves gpg

```sh
zypper --gpg-auto-import-keys refresh
```

Si lo requerimos, podemos actualizar el dominio de nuestro host

```sh
hostnamectl
hostnamectl set-hostname <DOMAIN>
```

Para conocer la hora y de ser necesario, cambiarla

```sh
timedatectl

timedatectl list-timezones
timedatectl list-timezones | grep America

timedatectl set-timezone America/Mexico_City
```


---
## Instalar paquetes

```sh
# Tools
zypper in findutils-locate tar zip unzip p7zip git wget curl nano rsync neofetch tmux
# Network tools
zypper in net-tools netcat lsof nmap
```


---
## Gestor de paquetes `zypper`

Para instalar paquetes, podemos hacer uso del comando `zypper`

```sh
zypper install <PACKAGE>
zypper in <PACKAGE>
```

Para actualizar paquetes

```sh
zypper patch # (1)

zypper update # (2)
zypper up
```

1.  Instalar solo los parches necesarios
2.  Actualizar paquetes instalados


Desinstalar paquetes

```sh
zypper remove <PACKAGE>
zypper rm <PACKAGE>
```

Buscar un paquete

```sh
zypper search <PATTERN>
zypper se <PATTERN>
```

Manejando repositorios

```sh
zypper repos, lr # (1)
zypper addrepo, ar # (2)
zypper removerepo, rr # (3)
zypper modifyrepo, mr # (4)
zypper refresh, ref # (5)
zypper clean, cc # (6)
```

1.  Visualizar todos los repositorios definidos
2.  Agregar un nuevo repositorio
3.  Eliminar un repositorio
4.  Modificar un repositorio
5.  Actualizar todos los repositorio
6.  Limpiar cache local


