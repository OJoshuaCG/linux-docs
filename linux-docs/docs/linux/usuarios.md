## Crear usuario

Si necesitamos crear un usuario "comun" sin permisos especiales, podemos realizar lo siguiente:

```sh
sudo useradd <USER>

sudo useradd -m <USER> # (1)

su <USER> # (2)
su - <USER> # (3)
```

1.  Con el flag `-m` permite crear el directorio del usuario
2.  Permanecemos en el directorio en el que nos encontremos
3.  Nos movemos al directorio `home` del usuario

!!! note "Nota"
    Este tipo de usuarios no podra modificar archivos o carpetas fuera de su carpeta default `/home/<USERNAME>` asi como no poder usar el comando `sudo`


Si necesitamos que pueda ejecutar el comando `sudo` debemos agregarlo al grupo de usuarios `sudo`

```sh
sudo usermod -aG sudo <USER>
```

---

## Crear usuario con privilegios root

Este metodo, lo que realiza es crear un usuario espejo root, esplicando cada "flag", tenemos:

- `-u` : Asignamos el `UID = 0`, mismo que le pertenece al usuario `root`.
- `-o` : Permite asignar un `UID` que ya esta asignado a otro usuario.
- `-g` : Asignamos el grupo de usuarios `root`.
- `-s` : Especificamos la terminal que queremos asignarle al usuario.

```sh
sudo useradd -u 0 -o -g 0 -s /bin/bash <USER>
sudo passwd <USER>
```

<!--
Forma comun

```sh
sudo useradd -m <USER>
# Despues de esto, se debera configurar ingresando contraseña y otros datos
sudo usermod -aG sudo <USER>

sudo /usr/sbin/visudo
# or
sudo visudo

    # User privilege specification
    root            ALL=(ALL:ALL) ALL
    <USERNAME>    	ALL=(ALL:ALL) ALL
```
---
-->


---

## Crear carpeta

Si al crear un usuario, no contamos con una carpeta o no pasamos el parametro `-m`, podemos seguir los siguientes pasos:

```sh
sudo mkdir /home/<USER>
sudo chown -R <USER>:root /home/<USER>
cp /etc/skel/.* /home/<USER>/ # (1)
```

1.  Copiamos 'dotfiles' comunes para el usuario


---

## Modificar usuario

Si necesitamos modificar el usuario, como su carpeta o terminal, podemos ejecutar los siguientes comandos:

```sh
sudo usermod -l <NEW_USER> <OLD_USER> # (1)
sudo usermod -d /home/<USER> # (2)
sudo usermod -s /bin/bash <USER> # (3)
sudo usermod -u <NEW_UID> <USER> # (4)
sudo usermod -L <USER> # (5)
sudo usermod -U <USER> # (6)
```

1.  Modificar nombre del usuario, por ejemplo `-l new_john john_doe`
2.  Modificar directorio `home`
3.  Modificar shell a usar
4.  Modificar `UID` del usuario
5.  Bloqueamos el usuario
6.  Desbloqueamos el usuario


---

## Eliminar usuario

Antes de eliminar un usuario, debemos asegurarnos que no tiene como propiedad un directorio de otro usuario, despues podemos eliminar al usuario utilizando las siguientes banderas:

- `-r` : Eliminar directorio del usuario
- `-f` : Forzar eliminacion

```sh
sudo userdel <USER>

sudo userdel -r <USER>

sudo userdel -f <USER>

sudo userdel -f -r <USER>
```

!!! warning "Problema"
    Si obtenemos el error `userdel <USER> is currently used by process <X>`
    debemos "matar" el(los) proceso(s) con los comandos

    ```sh
    sudo killall -u <USER>
    sudo kill -9 <X>
    ```


## Visualizar informacion del usuario

Si necesitamos conocer la informacion de un usuario en especifico:

```sh
id <USER>
getent passwd <USER>
```

Si queremos ver todos los usuarios creados:

```sh
less /etc/passwd
```


---

## Grupos

Si queremos conocer los grupos a los que pertenece un usuario:

```sh
groups <USER>
```

Para agregar un usuario a un grupo podemos utilizar el comando siguiente:

```sh
sudo usermod -aG <GROUP> <USER>
```

Para cambiar el grupo primario de un usuario:

```sh
sudo usermod -g <GROUP> <USER>
```

Si queremos remover un usuario de un grupo:

```sh
sudo gpasswd -d <username> <groupname>
```


---

## Sources

- [https://geekflare.com/es/user-management-in-linux/](https://geekflare.com/es/user-management-in-linux/)
- [https://es.stackoverflow.com/questions/46587/c%C3%B3mo-puedo-eliminar-el-usuario-root-en-un-servidor-web](https://es.stackoverflow.com/questions/46587/c%C3%B3mo-puedo-eliminar-el-usuario-root-en-un-servidor-web)
- [https://www.ionos.mx/ayuda/servidores-cloud/administracion-del-servidor/crear-un-usuario-con-permisos-sudo/](https://www.ionos.mx/ayuda/servidores-cloud/administracion-del-servidor/crear-un-usuario-con-permisos-sudo/)