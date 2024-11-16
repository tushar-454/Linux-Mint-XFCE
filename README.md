# Linux Mint XFCE Installation and Setup Guide

This guide provides detailed instructions on how to install and set up Linux Mint XFCE 64-bit, including software, themes, icons, and other configurations, especially useful for a MERN stack developer.

## Download Linux Mint XFCE

To get started, download the official Linux Mint XFCE ISO from the [Linux Mint Download Page](https://www.linuxmint.com/download.php).

For this guide, I'm using XFCE since it is lightweight and more performance-focused, consuming less CPU and RAM. Cinnamon, on the other hand, is heavier and more feature-rich, so it may not be the best choice for older or resource-limited hardware.

## Create a Bootable Pendrive

Once you've downloaded the ISO file, you will need to create a bootable USB drive. On Windows, you can use **Rufus**, and on Linux, **balenaEtcher** works well.

### Steps for Rufus (on Windows):
1. [Download Rufus](https://rufus.ie/downloads/).
2. Install and open Rufus.
3. Insert your USB drive.
4. In Rufus, select your USB device and the downloaded ISO file.
5. Choose the correct partition scheme for your system (GPT for UEFI or MBR for legacy BIOS).
6. Optionally, you can change the label for your USB.
7. Click "Start" to create the bootable USB drive.

### Steps for balenaEtcher (on Linux):
1. Install and open [balenaEtcher](https://www.balena.io/etcher/).
2. Select the ISO file and the USB drive.
3. Click "Flash" to create the bootable drive.

## Boot Linux Mint XFCE from Pendrive

Once you've created the bootable pendrive, plug it into the target machine and boot from it. You can usually access the boot menu by pressing a key like **F12** or **ESC** during startup, depending on your system's manufacturer.

You can try Linux Mint XFCE live before installation, and if you decide to proceed with installation, follow these steps:

1. **For a clean installation**, select "Erase disk and install Linux Mint." This is the easiest option, but it will remove all data on your hard drive, so ensure you've backed up your data.
2. **For a dual-boot setup**, select the "Something else" option to partition your drive manually. For dual-boot, you need unallocated space on your drive, which you can create using Windows' disk management tool. In this example, we allocate 70GB for Linux Mint.

Partition setup:
- **35GB** - ext4 - Mount point: `/` (root)
- **30GB** - ext4 - Mount point: `/home` (for personal files)
- **300MB** - EFI - Mount point: `/boot/efi` (for UEFI boot)
- **8GB** - swap - Used as swap memory (optional but recommended for systems with low RAM)

Once you've created the partitions, select the correct boot storage device and click "Install."

After installation, reboot the system, remove the USB drive, and boot into your new Linux Mint XFCE system.

## Linux Mint XFCE Setup After Installation

After installation, follow these steps to set up your system for development, especially for a MERN stack setup.

### 1. Update System
Run the following command to ensure your system is fully updated:
```bash
sudo apt update && sudo apt upgrade -y
