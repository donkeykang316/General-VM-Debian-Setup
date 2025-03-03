# CL for basic setup (Bookworm 12)
### sudo right
check the if the user within the sudo user group
```
getent group docker
```
add user to the sudo groupe in case its not ther
```shell
su
sudo usermod -aG sudo $USER
exit
```
if sudo right is still not enable for the user, enter root mode and use visudo command opens the /etc/sudoers file
```
sudo visudo
```
add the user to the sudoer file
```txt
user_name    ALL=(ALL:ALL) ALL
```
### install the essentials
```
sudo apt update && sudo apt upgrade -y && sudo apt install -y build-essential
```
### enable shared clipboard, drag-drop and shared folder with host
Ensures Guest Additions modules are rebuilt for kernel updates
```
sudo apt install -y dkms
```
Matches the kernel headers to your current kernel version
```
sudo apt install -y linux-headers-$(uname -r)
```
Mount and Run the Guest Additions Installer: The Guest Additions CD should appear as a mounted device (e.g., /media/<username>/VBox_GAs_<version>). If not, mount it manually
```
sudo mkdir -p /mnt/cdrom
sudo mount /dev/cdrom /mnt/cdrom
```
Run the isnatller
```
cd /mnt/cdrom
sudo sh ./VBoxLinuxAdditions.run
```
restart the VM
```
sudo reboot
```
- Under "Devices", set bidirectional to both "Shared Clipboard" and "Drag and Drop". Then select "Insert Guest Addtional CD Image" and then "Upgrade Guest Addtions".
- Under "Devices", create and mount the shared folder, if the folder isnt accessible after setup, follow the instruction bewlow
- check if "vboxsf" is listed in the group
```
groups
```
- if not, add the group manualy
```
sudo usermod -aG vboxsf $USER
```
- reboot the VM and login to recheck the groups