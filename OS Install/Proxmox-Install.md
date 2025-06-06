# Proxmox Install 
Proxmox install guild using a computer, USB drive, montor, and keyboard

## Minimum Devices, parts, and software required:
- Computer with internet connection
- Rufus or similar program
  - Download Here: https://rufus.ie/en/
- Bootable Device (USB/CD/DVD)
- Computer/Server Proxmox will be installed onto
- Digital Interface cord (HDMI/Display Port/USB-C, etc...)
- Montor 
- Keyboard (Corded or USB Dongle)

# Install Steps
1- Downlaod Proxmox ISO from website
  - https://www.proxmox.com/en/products/proxmox-virtual-environment/get-started
2- Insert bootable device (USB/CD/DVD) into computer 
3- Open Rufus and allow it to make changes on your device*
  - *The Proxmox ISO image HAS TO BE INSTALLED THOUGH RUFUS or a similar program. The computer will NOT boot though USB if ISO file is just copied to the bootable device.
4- Select the Proxmox ISO file and install it to the bootable device
5- When Rufus finishes formating and installing onto the device, remove it from the computer
6- Insert the bootable device into the computer you wish to install Proxmox onto
  - The computer must be poweroff
  - Must be plugged into a montor and keyboard (if not able to connect these devices, stop and refer to Proxmox Get Started Guild)
7- Power the computer on and interrupt the boot squence when prompted
8- In the new menu, pick to boot from bootable device and select the device with the ISO image installed
9- Allow the computer to reboot without interruption
10- Follow the directions on screen to finish the setup
11- Enter the provided IP address of the server into a computer brower and login using username and password setup during install process
