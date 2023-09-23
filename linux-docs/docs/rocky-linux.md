##  Post Instalacion

### Añadir un usuario nuevo

```sh
sudo su
adduser <USERNAME>
passwd <USERNAME>
usermod -aG wheel <USERNAME>
```

## Instalar paquetes

Rocky linux utiliza los gestores de paquete `dnf` y `yum`.

```sh
dnf update -y
dnf install epel-release cockpit firewalld wget curl nano -y
```

```sh
systemctl enable --now firewalld
systemctl enable --now cockpit
```

```sh
ip a

    inet 192.168.1.77/24
```

Para acceder al servidor, debemos abrir el navegador e ingresar el IP junto con el puerto `9090`. Por ejemplo: `<IP_ADDRESS>:9090`

[192.168.1.77:9090](http://192.168.1.77:9090)

**Cambiar Hostname:**

```sh
hostnamectl set-hostname <HOSTNAME>
```


---
### Allow ssh
```sh
nano etc/ssh/sshd_config

    PermitRootLogin yes

systemctl restart sshd.service
```


---
### Apache
```sh
dnf install httpd
systemctl enable httpd && systemctl enable httpd
```


### ERRORs

```sh
echo '#!/bin/sh' > /usr/sbin/sendmail
chmod +x /usr/sbin/sendmail

yum install bind-utils -y
```


---
### csf on Rocky Linux
```sh
dnf install perl wget curl nano -y
dnf install perl-libwww-perl.noarch perl-LWP-Protocol-https.noarch perl-Time-HiRes -y

cd /usr/src
wget https://download.configserver.com/csf.tgz
tar xzf csf.tgz
cd csf
sh install.sh

perl /usr/local/csf/bin/csftest.pl
csf -v

nano /etc/csf/csf.conf
    # lfd will not start while this is enabled
    TESTING = "0"

    # Allow incoming TCP ports
    TCP_IN = "20,21,22,25,53,80,110,143,443,465,587,993,995,9090"

    # Allow outgoing TCP ports
    TCP_OUT = "20,21,22,25,53,80,110,113,443,587,993,995,9090"


systemctl enable csf && systemctl enable lfd
systemctl start csf && systemctl restart lfd

systemctl status csf
systemctl status lfd
csf -e
```

`ff:ff:ff:ff:ff:ff:8c:ea:48:3c:ac:78:08:00`



## _Sources_
- [Docs Rocky Linux - firewalld](https://docs.rockylinux.org/es/guides/security/firewalld-beginners/)
- [DigitalOcean](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-rocky-linux-8)
- [How to install cockpit](https://www.howtoforge.com/how-to-install-cockpit-on-rocky-linux-8/)
- [Manage Rocky Linux using cockpit](https://computingforgeeks.com/manage-rocky-linux-using-cockpit-web-console/)