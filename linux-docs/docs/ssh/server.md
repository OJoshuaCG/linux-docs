## Instalacion

Se instalara el paquete `openssh`, esto puede variar dependiendo la distribucion:

```sh
# Debian
apt install openssh-server

# Rocky Linux
dnf install openssh-server

# Open Suse
zypper install openssh
```


---
## Configuracion

Lo primero que haremos sera habilitar el servicio para poder ingresar a nuestro servidor.

```sh
sudo systemctl start sshd
sudo systemctl enable sshd
```

Ahora editaremos el archivo `sshd_config` para ingresar como `root`

```sh
sudo nano /etc/ssh/sshd_config

  PermitRootLogin yes
```

Al finalizar, vamos a reiniciar el servicio.


```sh
sudo systemctl restart sshd
```

!!! note "Nota"
    En Debian no es posible ingresar con el usuario root, solo por medio de otro usuario


---
## Permitir accesos

Algunas de las configuracion que podemos realizar, sera bajo el archivo `sshd_config` donde podemos permitir el acceso a algunos usuarios o grupos de usuarios.

```sh
sudo nano /etc/ssh/sshd_config

  AllowUsers user1 user2 user3
  AllowGroups group1 group2 group3
  PermitRootLogin yes
  PasswordAuthentication yes

  UsePAM yes
```


---
## Bloquer accesos

Asi como podemos permitir accesos, tambien podemos bloquear a nivel de usuarios y grupos de usuarios.

```sh
sudo nano /etc/ssh/sshd_config

  DenyUsers user1 user2 user3
  DenyGroups group1 group2 group3
  PermitRootLogin no # No permitir acceso al usuario root
```

---
## sshd_config

Alguna configuracion extra que se puede configurar es la siguiente (todo en base del archivo `/etc/ssh/sshd_config`)

| Parametro                         | Valores      | Utilidad                                                        |
| --------------------------------- | ------------ | --------------------------------------------------------------- |
| `AuthorizedKeysFile`              | `/path/file` | Archivo que contiene las claves publicas                        |
| `Banner`                          | `/path/file` | Archivo para mostrar como pantalla de presentacion              |
| `ChallengeResponseAuthentication` | `yes`, `no`  | Permite la autentificacion a través de PAM                      |
| `HostKey`                         | `/path/file` | Archivos donde se guardan las Keys                              |
| `ListenAddress`                   | `hosts`      | Direcciones IP que tienen permitido conectarse                  |
| `LoginGraceTime`                  | `number`     | Tiempo maximo de espera para ingresar una contraseña            |
| `MaxAuthTries`                    | `number`     | Maximo numero de intentos para ingresar la contraseña           |
| `MaxSessions`                     | `number`     | Sesiones abiertas de Shell                                      |
| `MaxStartups`                     | `number`     | Sesiones maximas por IP/Host                                    |
| `PasswordAuthentication`          | `yes`, `no`  | Ingresar via ssh con una contraseña de usuario                  |
| `PermitEmptyPasswords`            | `yes`, `no`  | Aprobar contraseñas vacias                                      |
| `PermitRootLogin`                 | `yes`, `no`  | Ingresar con el usuario root                                    |
| `PubkeyAuthentication`            | `yes`, `no`  | Permite la autentificacion por clave publica                    |
| `UsePrivilegeSeparation`          | `yes`, `no`  | Separa privilegios por medio de un proceso hijo sin privilegios |



```sh
# /etc/ssh/sshd_config
Port 22
PermitRootLogin yes
PasswordAuthentication yes
PubkeyAuthentication yes

LoginGraceTime 30
MaxAuthTries 2
MaxSessions 5
MaxStartups 3

UsePAM no
ChallengeResponseAuthentication no
```


---
## Clave publica

Para agregar una clave publica en nuestro servidor basta con copiar el archivo `.pub` que se encuentra en nuestro equipo local

```sh
ssh-copy-id -i ~/.ssh/id_rsa.pub user@host
```


Para eliminar esta clave, debemos eliminar la linea agregada del archivo:

```sh
nano ~/.ssh/authorized_keys
```


---
## Establecer timezone

```sh
timedatectl list-timezones
timedatectl list-timezones | grep America
timedatectl list-timezones | grep Mexico
sudo timedatectl set-timezone <TIMEZONE>
```


---
## Asignar hostname

```sh
hostnamectl
sudo hostnamectl set-hostname <HOSTNAME>


sudo nano /etc/hosts

  127.0.0.1   localhost <HOSTNAME>
```
