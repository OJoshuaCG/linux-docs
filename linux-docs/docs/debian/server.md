## Crear usuario root

```sh
sudo adduser <USERNAME>
# Despues de esto, se debera configurar ingresando contraseña y otros datos
sudo usermod -aG sudo <USERNAME>
```

---
## Configurar ssh

```sh
sudo apt install openssh-server
sudo systemctl start sshd
sudo systemctl enable sshd

sudo nano /etc/ssh/ssh_config
  
  PermitRootLogin yes
  PermitRootLogin without-password

sudo systemctl restart sshd
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
