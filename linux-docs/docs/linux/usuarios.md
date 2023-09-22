## Crear usuario

Si necesitamos crear un usuario "comun" sin permisos especiales, podemos realizar lo siguiente:

```sh
sudo useradd <USER>
# Crear directorio del usuario
sudo useradd -m <USER>
su <USER>
su - <USER>
```


!!! note "Nota"
    Este tipo de usuarios no podra modificar archivos o carpetas fuera de su carpeta default `/home/<USERNAME>` asi como no poder usar el comando `sudo`


Si necesitamos que pueda ejecutar el comando `sudo` debemos agregarlo al grupo de usuarios

```sh
sudo usermod -aG sudo <USER>
```


Si necesitamos modificar el usuario, como su carpeta o terminal, podemos ejecutar los siguientes comandos:

```sh
sudo usermod -s /bin/bash <USER>
sudo usermod -d /home/<USER>
sudo usermod -u <NEW_UID> <USER>
```

---

```sh
sudo useradd -u 0 -o -g 0 -s /bin/bash <USER>
sudo passwd <USER>
```

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

## Crear carpeta
```sh
sudo mkdir /home/<USER>
sudo usermod --shell /bin/bash --home /home/<USER> <USER>
sudo chown -R <USER>:root /home/<USER>
cp /etc/skel/.* /home/<USER>/
```

## Eliminar usuario

Antes de eliminar un usuario, debemos asegurarnos que no tiene como propiedad un directorio de otro usuario.

```sh
sudo userdel <USER>

sudo userdel --remove-home <USER>
sudo userdel -r <USER>

sudo userdel --force <USER>
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

## Ver usuario

```sh
getent passwd <USER>
less /etc/passwd
```

## Grupos de un usuario

```sh
groups <USER>
```


## Sources

- [https://geekflare.com/es/user-management-in-linux/](https://geekflare.com/es/user-management-in-linux/)
- [https://www.zeppelinux.es/eliminar-usuarios-en-linux-desde-la-linea-de-comandos/](https://www.zeppelinux.es/eliminar-usuarios-en-linux-desde-la-linea-de-comandos/)
- [https://es.stackoverflow.com/questions/46587/c%C3%B3mo-puedo-eliminar-el-usuario-root-en-un-servidor-web](https://es.stackoverflow.com/questions/46587/c%C3%B3mo-puedo-eliminar-el-usuario-root-en-un-servidor-web)
- [https://www.ionos.mx/ayuda/servidores-cloud/administracion-del-servidor/crear-un-usuario-con-permisos-sudo/](https://www.ionos.mx/ayuda/servidores-cloud/administracion-del-servidor/crear-un-usuario-con-permisos-sudo/)