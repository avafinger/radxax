## RockPi X custom kernel for testing

* Based on stable kernel

releases: https://github.com/avafinger/radxax/releases

* https://github.com/avafinger/radxax/releases/tag/5.16.6
* https://github.com/avafinger/radxax/releases/tag/5.16.7
* https://github.com/avafinger/radxax/releases/tag/5.17.0-rc2
* https://github.com/avafinger/radxax/releases/tag/5.16.8 (with some fixes to wifi)
* https://github.com/avafinger/radxax/releases/tag/5.16.9
* https://github.com/avafinger/radxax/releases/tag/5.12.8 (add support for wifi variant hw 1.41)
* https://github.com/avafinger/radxax/releases/tag/5.16.9-2 (add support for wifi variant hw 1.41, Bluetooth, sound)
* https://github.com/avafinger/radxax/releases/tag/5.17.0-rc4 (add support for wifi variant hw 1.41, Bluetooth, sound)
* https://github.com/avafinger/radxax/releases/tag/5.16.10-2 (add support for wifi variant hw 1.41, Bluetooth, sound)
* https://github.com/avafinger/radxax/releases/tag/5.17.0-rc5


## Updating wifi firmare

To improve wifi experience, update the wifi firmware (thanks to kotori)

        cd /usr/lib/firmware/brcm/
        sudo mv 'brcmfmac43455-sdio.ROCK Pi-ROCK Pi X.txt' 'brcmfmac43455-sdio.ROCK Pi-ROCK Pi X.txt.radxa'
        sudo wget https://raw.githubusercontent.com/radxa/rkwifibt/master/firmware/broadcom/AP6254/wifi/nvram_ap6254.txt -O "brcmfmac43455-sdio.Radxa-ROCK Pi X.txt"
        sudo mv brcmfmac43455-sdio.bin brcmfmac43455-sdio.bin.radxa
        sudo wget https://raw.githubusercontent.com/RPi-Distro/firmware-nonfree/bullseye/debian/config/brcm80211/cypress/cyfmac43455-sdio.bin -O brcmfmac43455-sdio.bin
        sudo wget https://raw.githubusercontent.com/RPi-Distro/firmware-nonfree/bullseye/debian/config/brcm80211/cypress/cyfmac43455-sdio.clm_blob -O brcmfmac43455-sdio.clm_blob

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
  

**Creating the USB stick**

* Dowload the file: rockpix_usb_ubuntu_20.04-4GB.img.7z
* Uncompress using 7z tools
* Burn the USB file img to the USB stick with your preferred tool
* In BIOS, choose Boot from USB
* You may need an RTC to save latest boot configuration


**Credentials**

     user:     ubuntu
     password: ubuntu


Download IMG file from here:

https://github.com/avafinger/radxax/releases/tag/usb-4GB
