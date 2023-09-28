## Configurar servidor ssh

```sh
sudo apt install openssh-server
sudo systemctl start sshd
sudo systemctl enable sshd

sudo nano /etc/ssh/ssh_config

  PermitRootLogin yes


sudo systemctl restart sshd
```


---
## Permitir accesos

```sh
sudo nano /etc/ssh/ssh_config

  AllowUsers user1 user2 user3
  AllowGroups group1 group2 group3
  PermitRootLogin yes
  PasswordAuthentication yes

  UsePAM yes
```


---
## Bloquer accesos

```sh
sudo nano /etc/ssh/ssh_config

  DenyUsers user1 user2 user3
  DenyGroups group1 group2 group3
  PermitRootLogin no
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
