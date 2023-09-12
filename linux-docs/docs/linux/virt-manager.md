## CLI

**All command will be executed in libvirt images location `/var/lib/libvirt/images` and conecting with qemu system `-c qemu:///system`**
```sh
cd /var/lib/libvirt/images
--
``` 


Install a Virtual Machine
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


Actions in Virtual Machine
```sh
# Run/Start
virsh --connect qemu:///system start vm_name
# Reboot
virsh --connect qemu:///system reboot vm_name
# Shutdown/Turn Off
virsh --connect qemu:///system shutdown vm_name
# Force Shutdown
virsh --connect qemu:///system destroy vm_name
```


View all Virtual Machines created

```sh
cd /var/lib/libvirt/images/
virsh -c qemu:///system list --all
```


### Snapshots

```sh
# Create snapshot 
virsh -c qemu:///system snapshot-create-as vm_name snapshot_name

# View snapshots
virsh -c qemu:///system snapshot-list vm_name

# Restore snapshot
virsh -c qemu:///system snapshot-revert vm_name snapshot_name

# Delete snapshot 
virsh -c qemu:///system snapshot-delete vm_name snapshot_name

# Get snapshot info
virsh -c qemu:///system snapshot-info vm_name snapshot_name
```


### View ip address from VM

```sh
virsh -c qemu:///system net-list
virsh -c qemu:///system net-info default
virsh -c qemu:///system net-dhcp-leases default
```



Open Suse Leap

sudo zypper ref && sudo zypper up
zypper update
sudo zypper --gpg-auto-import-keys refresh
apt install locate tar zip unzip p7zip git wget curl rsync 
