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

### nodejs

Para instalar nodejs debemos adjuntar la version `nodejsVERSION`, esto instalara `nodejs` y `npm`

```sh
zypper install nodejs18
```

### python

```sh
zypper install python311
```

### php

```sh
zypper install php8 php8-cli php8-curl php8-dba php8-intl php8-mbstring php8-zip php8-pdo php8-mysql php8-pgsql
```


---
## Gestor de paquetes `zypper`

Para instalar paquetes, podemos hacer uso del comando `zypper`


| Comando                             | Accion                                                   |
| ----------------------------------- | -------------------------------------------------------- |
| `zypper install/in <PACKAGE>`       | Instalar un paquete                                      |
| `zypper update/up <PACKAGE>`        | Actualizar paquetes instalados                           |
| `zypper patch <PACKAGE>`            | Actualizar parches/paquetes necesarios                   |
| `zypper remove/rm <PACKAGE>`        | Remover un paquete                                       |
| `zypper search/se <PATTERN>`        | Buscar coincidencias del 'patron' entre los repositorios |
| `zypper search/se --installed-only` | Visualizar paquetes instalados                           |
| `zypper info/if <PACKAGE>`          | Obtener informacion de un paquete                        |
| `zypper packages/pa`                | Listar todos los paquetes disponibles (instalados y no)  |
| `zypper repos/lr`                   | Visualizar todos los repositorios definidos              |
| `zypper addrepo/ar`                 | Agregar un nuevo repositorio                             |
| `zypper removerepo/rr`              | Eliminar un repositorio                                  |
| `zypper modifyrepo/mr`              | Modificar un repositorio                                 |
| `zypper refresh/ref`                | Actualizar todos los repositorios                        |
| `zypper clean/cc`                   | Limpiar cache local                                      |
