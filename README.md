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
```

**_📌 install updated ubuntu recommended GPU driver & reboot_**

**2.Install Git and Setup**

```bash
sudo apt install git
git --version
```

**3. Configure Git)**

```bash
git config --global user.name "Your username"
```

```bash
git config --global user.email "Your email"
```

**4. For create another firefox profile**

```bash
firefox -p
```

**5. Generate a New SSH Key**

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
cat ~/.ssh/id_ed25519.pub
```

**_If ed25519 not supported_**

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
cat ~/.ssh/id_rsa.pub | xclip -selection clipboard
```

Then You found a ssh key copy it then go to github setting under ssh keys section you add copy ssh key there and save it.
**_Test github connection_**

```bash
ssh -T git@github.com
```

you can see this message if success **_Hi username! You've successfully authenticated, but GitHub does not provide shell access._**
**\*If you clone your github repo using HTTPS then replace url with SSH**

```bash
git remote set-url origin git@github.com:username/repo.git
```

Now it's work push/pull without username/password promt also new clone repo using SSH insted of HTTPS

**6. Install VS Code**

```bash
sudo apt update && sudo apt upgrade -y
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor -o packages.microsoft.gpg
sudo install -o root -g root -m 644 packages.microsoft.gpg /usr/share/keyrings/
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" | sudo tee /etc/apt/sources.list.d/vscode.list
sudo apt update
sudo apt install code -y
sudo apt update && sudo apt upgrade -y
code
```

**7. Change the default theme enable dark mode**
`Settings > Appearance > Mint-Y-Dark-Aqua`
`Settings > Window Manager > Mint-Y-Dark-Aqua`
**8. Turn on VS Code setting sync by sign in with GitHub**

**9. Install Node.js using (NVM)**

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash
source ~/.bashrc
nvm --version
```

**_Install nodejs lts version_**

```bash
nvm install --lts
node --version
npm --version
```

**_Install other version of nodejs_**

```bash
nvm install 18.20.5
nvm use 18.20.5
node --version
npm --version
```

**_Install yarn_**

```bash
npm install --global yarn
yarn --version
```

**10. Install VLC**

```bash
sudo apt install vlc
```

**11. Install custom fonts**
[Downlaod Font](https://1drv.ms/f/c/1b6b9205ab056810/EsM7ojuV4rdBkmSpQLgl-90Bz9QlMawKwaehJ5mfrMSFqw?e=9IDNtM)

```bash
cd /usr/share/fonts/
```

open folder as root
then move your font file here then run `systemctl reboot`

**12. Setup Timezone and format**

right click on time and date then click on `Digital Clock Settings` then set your timezone and format

**13. Customise Panel**

Right click on panel then click on `Panel` then click on `Panel Preferences` then click on `Items` then add `Separator` then add `Whisker Menu` then add `Window Buttons` then add `Workspace Switcher` then add `Notification Area` then add `PulseAudio Plugin` then add `Battery Monitor` then add `Clock` then click on `Appearance` then select `Solid color` then select `Background color` then click on `Advanced` then select `Transparent` then click on `OK` then click on `Close`

Under `Whisker Menu` click on `Edit Icon` then customize as you want.

![Whisker-menu-image](https://res.cloudinary.com/dcdfbratw/image/upload/v1731779872/whisker_menu_setup_ybpwpz.png)

**14. Install MongodbCompass**

Go to [MongodbCompass](https://www.mongodb.com/try/download/compass) select latest version and platform ubuntu then copy link

```bash
wget past link here
```

```bash
sudo dpkg -i <file_name.deb>
```

**15. Add desktop wallpaper**
[Download Wallpaper SNOW](https://1drv.ms/i/c/1b6b9205ab056810/ERBoBasFkmsggBuIAAAAAAABSsCn1fUlLKZYg9qEk4PE0A?e=zpJ7O4)

**16. Install Codeblocks**

```bash
sudo add-apt-repository ppa:codeblocks-devs/release
sudo apt update
sudo apt install codeblocks
codeblocks --version
codeblocks
```

```bash
sudo apt update
sudo apt install gfortran
gfortran --version
sudo apt install build-essential
gfortran program.f90 -o program
```

for gfortran path run `which gfortran`
configure codeblocks for gfortran path `Settings > Compiler > Select GNU Fortran Compiler set as default > Toolchain executables` then set path `/usr/bin` then click on `OK`

**17. Install Discord**

```bash
wget https://stable.dl2.discordapp.net/apps/linux/0.0.74/discord-0.0.74.deb
sudo dpkg -i <file_name.deb>
discord
```

**18. Install Slack**

```bash
sudo apt update
sudo apt install alien
wget https://downloads.slack-edge.com/desktop-releases/linux/x64/4.41.97/slack-4.41.97-0.1.el8.x86_64.rpm
sudo alien -d <file_name.rpm>
sudo dpkg -i <file_name.deb>
sudo apt-get install -f
slack
```

**19. Clear unnecessary packages files folders**

```bash
sudo apt-get autoremove
sudo apt-get clean
```

```bash
npm cache clean --force
```

**20. Install postman**

```bash
wget https://dl.pstmn.io/download/latest/linux_64?deviceId=Suc3jbLBgDbLAMwAv6zXam
sudo tar -xvf <file_name.tar.gz>
sudo mv Postman /opt/
sudo ln -s /opt/Postman/Postman /usr/bin/postman
postman
```

**21. Install Mongodb Server Local**

```bash
wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-ubuntu2204-8.0.3.tgz
sudo tar -zxvf <file_name.tgz>
sudo mv <file_name> /opt/mongodb
```

```bash
sudo mkdir -p /var/lib/mongo
sudo chown -R mongodb:mongodb /var/lib/mongo
sudo mkdir -p /var/log/mongodb
sudo chown -R mongodb:mongodb /var/log/mongodb
```

```bash
sudo nano /etc/systemd/system/mongod.service
```

```
[Unit]
Description=MongoDB Database Server
Documentation=https://docs.mongodb.org/manual
After=network.target

[Service]
ExecStart=/opt/mongodb/bin/mongod --dbpath /var/lib/mongo --logpath /var/log/mongodb/mongod.log --bind_ip_all
User=mongodb
Group=mongodb
PIDFile=/var/run/mongodb/mongod.pid
Restart=always

[Install]
WantedBy=multi-user.target

```

```bash
sudo systemctl daemon-reload
sudo systemctl start mongod
sudo systemctl status mongod
```

```bash
sudo systemctl enable mongod # to start mongodb on boot
```

**_if not running_**

```bash
sudo groupadd mongodb
sudo useradd --no-create-home --shell /bin/false -g mongodb mongodb
id mongodb
```

```bash
sudo chown -R mongodb:mongodb /var/lib/mongo
sudo chown -R mongodb:mongodb /var/log/mongodb
```

```bash
sudo systemctl restart mongod
sudo systemctl status mongod
```

**_mongod server start_**

```bash
sudo systemctl start mongod
```

**_mongod server stop_**

```bash
sudo systemctl stop mongod
```

**22 Password change linux user**

```bash
passwd
sudo passwd username # change another user password
```

**22. Install Avro Phonetic for Linux**
[ibus-avro](https://linux.omicronlab.com/)

```bash
sudo apt-get install ibus-avro
```

```bash
ibus-setup
```

then under `input method` click on `add` then select `Bangla` then select `Avro Phonetic` then click on `Add` then click on `Close` then `reboot system`

**23. Install Telegram**
Downlaod telegram from [Telegram](https://telegram.org/dl/desktop/linux)

```bash
sudo tar -xf <file_name.tar.xz>
```

```bash
sudo mkdir -p /opt/telegram
sudo mv Telegram/* /opt/telegram
sudo ln -s /opt/telegram/Telegram /usr/local/bin/telegram
telegram
```

**24. Install Zoom**
Donwload zoom from [Zoom](https://zoom.us/download)

```bash
sudo dpkg -i <file_name.deb>
sudo apt --fix-broken install
zoom
```
