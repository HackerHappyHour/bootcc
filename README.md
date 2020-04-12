### Steps
1. insert usb disk
1. download ubuntu image
1. get disk device map designation using `lsblk -a -d -e7`
1. example device is `/dev/sde`
1. uncompress and pipe ubuntu compressed disk image to `dd` to "restore" it to usb disk
1. `xzcat ubuntu.img.xz | sudo dd status=progress of=/dev/sde bs=4M conv=nowarn,sync`
1. `touch /media/${USER}/system-boot/ssh` to enable ssh
1. Edit `/media/${USER}/system-boot/network-config` to include wireless info
(see below)
1. `sudo touch /media/${USER}/writable/etc/wpa_supplicant/wpa_supplicant.conf`
1. add a `network` config to `wpa_supplicant.conf` file just created
1. Turn on pi, wait ~1 minute for boot
1. login using `ssh ubuntu@<static_ip_address (declared below in netplan example)>` with password `ubuntu`
1. Follow prompts to change password immediately, will disconnect after password is updated
1. log back in using `ssh ubuntu@<static_ip_address>` with the new password, and voila!


Following example taken directly from [netplan.io/examples#conecting-to-a-wpa-personal-wireless-network]()

Edit the `system-boot/network-config` file as follows:

```yaml
... # existing config
  wifis:
    wlan0:
      optional: true
      dhcp4: no
      dhcp6: no
      addresses: [192.168.0.21/24]
      gateway4: 192.168.0.1
      nameservers:
        addresses: [192.168.0.1, 8.8.8.8]
      access-points:
        "network_ssid_name":
          password: "**********"
```

example `etc/wpa_supplicant/wpa_supplicant.conf`

```conf
network={
    ssid="ssidname"
    psk="password"
}
```

### Links

https://wiki.ubuntu.com/ARM/RaspberryPi
https://www.raspberrypi.org/documentation/configuration/config-txt/README.md
https://netplan.io/examples#connecting-to-a-wpa-personal-wireless-network
