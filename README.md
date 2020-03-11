### Steps
1. insert usb disk
1. download ubuntu image
1. get disk device map designation using `lsblk -a -d -e7`
1. example device is `/dev/sde`
1. uncompress and pipe ubuntu compressed disk image to `dd` to "restore" it to usb disk
1. `xzcat ubuntu.img.xz | sudo dd status=progress of=/dev/sde bs=4M conv=nowarn,sync`
1. `touch system-boot/ssh` to enable ssh
1. (Optional) Create netplan with static IP so you don't have to look up ip of raspberry pi using router
 - Disable cloud-init using 

### Links

https://wiki.ubuntu.com/ARM/RaspberryPi
https://www.raspberrypi.org/documentation/configuration/config-txt/README.md
