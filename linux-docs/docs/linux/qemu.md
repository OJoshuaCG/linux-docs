## Instalar Qemu

```sh
sudo pacman -Syy
sudo pacman -S archlinux-keyring
sudo pacman -S qemu-desktop virt-manager virt-viewer dnsmasq vde2 bridge-utils openbsd-netcat dmidecode

sudo pacman -S libguestfs

sudo systemctl enable libvirtd.service
sudo systemctl start libvirtd.service
systemctl status libvirtd.service

sudo usermod -a -G libvirt $(whoami)
sudo systemctl restart libvirtd.service
```

Con esto, podemos abrir `Virtual Machine Manager`


_**Fuentes:**_

- [https://www.youtube.com/watch?v=D6_95M7_8Rg](https://www.youtube.com/watch?v=D6_95M7_8Rg)
- [https://computingforgeeks.com/install-kvm-qemu-virt-manager-arch-manjar/?expand_article=1](https://computingforgeeks.com/install-kvm-qemu-virt-manager-arch-manjar/?expand_article=1)


---
## CLI

Todos los comandos deben ejecutarse dentro de la ubicacion  de las imagenes de libvirt `cd /var/lib/libvirt/images` y ejecutarse realizando la conexion a qemu `virsh -c qemu:///system`

```sh
cd /var/lib/libvirt/images
virsh -c qemu:///system
```

### Instalar una maquina virtual

```sh
# Inline
virt-install --name fpbx --memory 2048 --vcpus 2 --disk /var/lib/libvirt/images/vm_name.qcow2,bus=sata --import --os-variant rockylinux8 --network default

# Multiline
virt-install \
--name $vm_name \
--disk path=/virt/kvm/vms/vm_name.qcow2,size=8 \
--vcpus 1 \
--ram 1024 \
--os-type linux \
--os-variant debian9 \
--network bridge=br0 \
--graphics spice \
--video qxl \
--channel spicevmc \
--console pty,target_type=serial \
--location 'http://ftp.us.debian.org/debian/dists/stable/main/installer-amd64/'
```


### Controlar maquina virtual

```sh
# Visualizar maquinas virtuales
virsh -c qemu:///system list --all

# Encender
virsh -c qemu:///system start vm_name

# Reiniciar
virsh -c qemu:///system reboot vm_name

# Apagar
virsh -c qemu:///system shutdown vm_name

# Forzar apagado
virsh -c qemu:///system destroy vm_name
```


### Consultar IP de la maquina virtual

```sh
virsh -c qemu:///system net-list
virsh -c qemu:///system net-info default
virsh -c qemu:///system net-dhcp-leases default
```


### Snapshots

```sh
# Crear una snapshot
virsh -c qemu:///system snapshot-create-as vm_name snapshot_name

# Ver snapshots de una maquina virtual
virsh -c qemu:///system snapshot-list vm_name

# Restaurar una snapshot
virsh -c qemu:///system snapshot-revert vm_name snapshot_name

# Eliminar una snapshot
virsh -c qemu:///system snapshot-delete vm_name snapshot_name

# Obtener la informacion de una snapshot
virsh -c qemu:///system snapshot-info vm_name snapshot_name
```
