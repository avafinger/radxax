## RockPi X custom kernel for testing

* Based on stable kernel

releases

* https://github.com/avafinger/radxax/releases/tag/5.16.6
* https://github.com/avafinger/radxax/releases/tag/5.16.7
* https://github.com/avafinger/radxax/releases/tag/5.17.0-rc2


## USB stick with Ubuntu 20.04.3 LTS (CLI) for RockPi X

A USB stick with efi partition with ubuntu 20.04.3 LTS for testing custom kernels.
It consist of
2 partitions:

    /dev/sde1            2048    1050623    1048576     512M EFI System         
    /dev/sde2         1050624    7888862    6838239     3,3G Linux filesystem

**linux partition**

The linux partiton holds the rootfs.
Wifi can be configured by editing the netplan file:

        /etc/netplan/00-installer-config.yaml
        
Edit the file with a linux editor and write down the SSID and password.
Do not change the layout.

 **Example:**

 * SSID: **FIBER-5G**
 * password: **3aFd6GFzPw**

        # This is the network config written by 'subiquity'
        network:
          ethernets:
            enp1s0:
              dhcp4: true
          wifis:
              wlan0:
                access-points:
                  FIBER-5G:
                    password: 3aFd6GFzPw
                dhcp4: true
          version: 2
          

**EFI partition**

EFI partition is where the boot loader looks for grub.cfg and display the kernels to be loaded.
You will be presented a list of kernels, select the one you want to test and hit the [ENTER].

If you install a new kernel you may need to add a new entry manually.
  
        /boot/efi/EFI/BOOT/grub/grub.cfg
  
