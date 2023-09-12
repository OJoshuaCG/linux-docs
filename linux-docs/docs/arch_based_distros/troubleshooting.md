## invalid password

Si al comienzo de nuestro sistema, queremos instalar algo con `sudo` e ingresamos nuestra contraseña, podemos obtener el error `invalid password` el cual despues de 3 intentos deja de pedirnos la contraseña, para ello debemos actualizar el sistema con el comando `pacman -Syyu`.
Si esto sucede aun despues de actualizar el sistema, podemos cambiar la contraseña con el comando `passwd`.


---
## GLIBC_2.34 not found

Este es un problema que da mucho dolor de cabeza, para resolverlo primeramente y lo recomendable es NO apagar ni reiniciar el sistema.
Debemos de abrir nuestra terminal y actualizar el sistema, te puedes guiar con los siguientes comandos

```bash
su		# Ingresa tu contraseña de root
pacman -Syyu
```

Si esto no resuelve tu problema, lo mas probable es que debas reinstalar el SO.


---
## Paquete no válido o dañado (firma PGP)

```sh
sudo pacman -Syy
sudo pacman-key --refresh-keys
sudo pacman-key --populate archlinux
sudo pacman -Scc

sudo pacman -Syyu

sudo pacman -S archlinux-keyring
```


---
## Recordar ultimo SO seleccionado en Dual Boot

Esta configuracion se hace desde Linux, y es modificando el GRUB.

1. Haremos un backup de nuestro grub

   ```bash
   sudo cp /etc/default/grub ~/grub.bak
   ```

2. Editaremos la configuracion de nuestro grub `sudo nano /etc/default/grub` y agregamos/modificamos las siguientes lineas

    ```bash
    GRUB_DEFAULT=saved
    GRUB_SAVEDEFAULT=true
    ```

3. Aplicamos los cambios con el siguiente comando

    ```bash
    sudo update-grub
    ```


---

## Arreglar Boot de Windows y agregarlo al grub de Linux

### Windows

Ingresar a la consola de Windows por medio de una USB, cargando al ISO de Windows e iniciando una reparacion.

Primero verificamos si tenemos si se encuentra el boot cargado con el siguiente comando, si el resultado es "vacio", significa que no tenemos cargado algun boot de Windows

```sh
bcdedit
```

Dentro de la consola, primero seleccionamos la particion donde tenemos windows, y encontraremos la particion/volumen del EFI.

Suele reconocerse al tener el nombre de `System` o teniendo el Sistema de Archivos `FAT32`, y con la informacion oculta (`HIDDEN`)

```sh
diskpart
list disk
sel disk 0

list partition
# Partition #   System  99 MB   offset

list volume
# Volume #      FAT32   Partition   99 MB   Healthy Hidden
```

Nos aseguramos que tengamos las carpatas como Program Files, Users, Windows.

```sh
dir C:\
```

Asignamos una letra a nuestra particion EFI y luego nos salimos de `diskpart`

```sh
select volume #
assign letter K:

exit
```

#### Opcion 1:

Nos aseguramos de estar en la carpeta Sources de la USB boot para reparar el boot con el siguiente comando:

```sh
cd /d X:\Sources

attrib BCD -s -h -r
ren BCD BCD.bak
bcdboot C:\Windows /l es-mx /s k: /f ALL

bcdedit
# Observaremos el boot de Windows como resultado
```

#### Opcion 2:

Nos dirigimos al bootloader y buscamos el boot con alguno de los siguientes comandos:

```sh
cd /d K:\efi\microsoft\boot\

cd /d K:\Boot\

cd /d K:\ESD\Windows\EFI\Microsft\Boot\
```

En algunos casos pueden ejecutar uno de los siguientes comandos para sobreescribir la particion boot

```sh
bootrec /fixboot
bootrec /scanos
bootrec /rebuildbcd
# or
bootrec /FixMbr
```


### Linux

Abrir la terminal y ejecutar los siguientes comandos:

```sh
sudo os-prober
sudo update-grub
```

Reiniciar y verificar si ya se encuentra la opcion para bootear en Windows

- _**Fuente** [Reparar UEFI Boot en Windows 10](https://woshub.com/how-to-repair-uefi-bootloader-in-windows-8/)_


---
## Sincronizar relojes Windows y Linux

### Windows

Dentro del panel de control, nos dirigiremos a **Panel de control\Reloj y región** dentro seleccionaremos **Fecha y Hora > Hora de Internet > Cambiar la configuracion**, luego desactivamos la opcion de `Sincronizar con un servidor horario de Internet`.

Dentro de la configuracion de windows, desactivar la opcion `Establecer la zona horaria automaticamente`, la opcion `Establecer la hora automaticamente` no sera necesaria desactivarla, si despues de todo el proceso, no funciona, intenta desactivar esta opcion.

Abriremos el simbolo del sistema como administrador y ejecutaremos la siguiente linea

```bash
reg add "HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation" /v RealTimeIsUniversal /d 1 /t REG_DWORD /f
```


### Linux

Tendremos que tener instalado el paquete `ntp` para despues ejecutar el siguiente comando

```
sudo ntpd -qg
```

- _**Fuente:** [System Time - Arch Linux](https://wiki.archlinux.org/title/System_time)_


---
## No hacer nada al cerrar tapa (laptop)

Abrir el archivo `etc/systemd/logind.conf` con `nano` e ingresar la siguiente linea:
```bash
HandleLidSwitch=ignore
```

Luego abrir el siguiente archivo `/etc/UPower/UPower.conf` con `nano` e ingresar la siguiente linea:
```bash
IgnoreLid=true
```


---
## Eliminar _"Bloqueo de usuario despues de 'n' intentos"_

Este es un "problema" presente dentro de Linux agregado por temas de seguridad, el cual despues de realizar 3 intentos seguidos de inicio de sesion y ambos fallidos, nuestro usuario es bloqueado, teniendo que esperar 10 minutos para volver a iniciar sesion en ese usuario.

Para poder eliminar este problema, tendremos que modificar el archivo `faillock.conf` y agregar la siguientes lineas.

```bash
sudo nano /etc/security/faillock.conf

    # Lineas a agregar
    deny = 0            # Evitar bloquear usuario
    fail_interval = 30  # Esperar solo 30 segundos
    unlock_time = 10    # Desbloquear solo despues de 10 segundos
```
