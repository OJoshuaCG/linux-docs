## Otorgar privilegios root a tu usuario

Para poder instalar nuestros paquetes dentro de Debian ocupamos tener privilegios root, para ello, podemos entrar en el entorno `root` u otorgarle los privilegios a nuestros usuario de la siguiente forma

```sh
# Entrar como root
su - root
apt install sudo -y

# Crear usuario
usermod -aG sudo <USER>
su - <USER>
```

Sin cerrar la terminal, vamos a buscar actualizaciones de los paquetes, para despues descargar y actualizar los paquete.

```bash
sudo apt update
sudo apt upgrade -y
```

Si tenemos detalles con actualizar los paquetes, debemos eliminar las lineas en donde se incluyen los repositorios de `deb cdrom` dentro del archivo `/etc/apt/sources.list`

```bash
sudo nano /etc/apt/sources.list
```

Despues de esto, podemos intentar actualizar de nuevo nuestro sistema

```bash
sudo apt update && sudo apt upgrade -y
```

Al finalizar, reiniciaremos nuestra maquina, para aplicar los cambios de nuestro usuario

!!! warning "Advertencia"
    Si cerramos la terminal despues de darle privilegios `root` a nuestro usuario, se perderan, por lo que debemos iniciar de nuevo desde el comienzo (`su - root`)

---

## Agregando repositorios no oficiales

Para agregar mas enlaces a repositorios debemos crear un archivo `sources.list` dentro de la carpeta `/etc/apt/sources.list.d/` y lo realizaremos con `nano` (o el editor de texto de tu preferencia)

```bash
sudo nano /etc/apt/sources.list.d/sources.list
```

Dentro agregaremos las siguientes lineas donde:

- bullseye: Debian 11
- bookworm: Debian 12

```bash
# Non-free software
deb http://deb.debian.org/debian bullseye non-free non-free-firmware
deb-src http://deb.debian.org/debian bullseye non-free non-free-firmware

deb http://deb.debian.org/debian-security bullseye-security non-free non-free-firmware
deb-src http://deb.debian.org/debian-security bullseye-security non-free non-free-firmware

deb http://deb.debian.org/debian bullseye-updates non-free non-free-firmware
deb-src http://deb.debian.org/debian bullseye-updates non-free non-free-firmware

# Unofficial repositories https://wiki.debian.org/DebianRepository/Unofficial
# Deb Multimedia
# http://www.deb-multimedia.org/
deb https://www.deb-multimedia.org bullseye main non-free

# Linux Software Repository for Microsoft Products
# https://learn.microsoft.com/en-us/windows-server/administration/linux-package-repository-for-microsoft-software
deb https://packages.microsoft.com/debian/11/prod stable main
```

Procedemos a guardar el archivo y ejecutar el siguiente comando

```bash
sudo apt update
```

Si contamos con el error `the following signature could't be verified because the public key is not available`, ejecutaremos el siguiente comando en base a la clave dada

```bash
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys <PUBKEY>
```


---
## MPR (makedeb Package Repository)

[MPR](https://mpr.makedeb.org/) es un repositorio mantenido por los usuarios, similar a [AUR](https://aur.archlinux.org/) (ArchLinux User Repository) para distribuciones Arch.

- Primero debemos instalar el [`APT Repository makedeb`](https://docs.makedeb.org/installing/apt-repository/)
- Luego instalar [`makedeb`](https://docs.makedeb.org/installing/shell-script/)
- Despues instalaremos [`Prebuilt MPR`](https://docs.makedeb.org/prebuilt-mpr/getting-started/)
- Por ultimo, tendremos que instalar [`mist`](https://docs.makedeb.org/using-the-mpr/mist-the-mpr-cli/) a través del comando `sudo apt install mist`

Con esto, ahora podemos instalar paquetes con ayuda de `mist` a traves del comando `mist install <PACKAGE>`, los paquetes a poder instalar los encontramos [aqui](https://mpr.makedeb.org/)


---
## Paquetes

```bash
# Tools
sudo apt install locate tar zip unzip p7zip git wget curl rsync neofetch tmux -y
# Developers packages
sudo apt install build-essential gnupg -y
# Network tools
sudo apt install net-tools netcat lsof nmap -y
# Package manager via GUI
sudo apt install synaptic -y
# Utilities
sudo apt install thunderbird vlc filezilla -y

```


Usar `sudo apt install <package> <package> ...`

| Nombre del programa | Nombre del paquete |
| ------------------- | ------------------ |
| Visual Studio Code  | apt install code   |


## _Fuentes_

- [Top 12 cosas que hacer despues de la instalación Debian 11](https://www.linuxtechi.com/things-to-do-after-installing-debian-11/)
- [Instalar paquetes apt get](https://terminaldelinux.com/terminal/administracion/instalar-paquetes-apt-get/)
- [Instalar paquetes deb con dpkg debian](https://www.diversidadyunpocodetodo.com/instalar-paquetes-deb-con-dpkg-debian/)
- [Docs makedeb Package Repository](https://docs.makedeb.org/installing/release-types/)