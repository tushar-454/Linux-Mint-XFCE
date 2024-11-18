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

**25. Chrome Browser Install**

Download chrome browser from [Click here](https://www.google.com/chrome/)

```bash
sudo dpkg -i <file_name.deb>
sudo apt --fix-broken install
google-chrome
```

**26. Customise Terminal**

Install Oh My Posh

```bash
sudo wget https://github.com/JanDeDobbeleer/oh-my-posh/releases/latest/download/posh-linux-amd64 -O /usr/local/bin/oh-my-posh
sudo chmod +x /usr/local/bin/oh-my-posh
```

Donwload Nerd Font

```bash
wget -P ~/.local/share/fonts https://github.com/ryanoasis/nerd-fonts/releases/download/v3.0.2/FiraCode.zip
unzip ~/.local/share/fonts/FiraCode.zip -d ~/.local/share/fonts
fc-cache -fv
```

or do it manually, [Firacode Nerd Font](https://github.com/ryanoasis/nerd-fonts/releases/download/v3.0.2/FiraCode.zip)

_unzip the fle and move the font file in `/usr/share/fonts`_

_path must be open with root permission_

Go to the terminal preferences and change the font to the installed Nerd Font (e.g., "FiraCode Nerd Font").

```bash
nano ~/.bashrc
```

Add the following line to set an Oh My Posh theme:

```bash
eval "$(oh-my-posh init bash --config ~/.poshthemes/your-theme-name.omp.json)"

```

Create a themes directory:

```bash
mkdir ~/.poshthemes
```

```bash
wget https://github.com/JanDeDobbeleer/oh-my-posh/releases/latest/download/themes.zip -O ~/.poshthemes/themes.zip
unzip ~/.poshthemes/themes.zip -d ~/.poshthemes
chmod u+rw ~/.poshthemes/*.omp.json
```

apply theme

```bash
source ~/.bashrc
```

Also change font from terminal settings and `reboot`

if font not apply on vscode terminal _you need to move font in /usr/shared/fonts_

```bash
sudo cp ~/.local/share/fonts/FiraCodeNerdFont* /usr/share/fonts/
sudo fc-cache -fv
```

**27. Install sublime text**

Donwload sublime text from [Sublime Text](https://www.sublimetext.com/download)

```bash
sudo dpkg -i <file_name.deb>
subl
```

**28. Hibernate system**

```bash
sudo systemctl hibernate
```

**29. Check storage using command**

```bash
df -h # check storage
```

```bash
df -h /dev/sd* # check storage of specific drive
```

**30. Install clipman for clipboard history**

```bash
sudo apt install xfce4-clipman
xfce4-clipman
```

- After launching, you should see the clipboard icon in your system tray (panel).
- Right-click the icon to configure options or view history.
- Open the Clipman settings by right-clicking the icon in the system tray and selecting Properties.
- Enable "Keep clipboard history".
- Adjust the number of items you want to keep in the history.

You can bind a keyboard shortcut to quickly access clipboard history:

- Go to Settings > Keyboard > Application Shortcuts.
- Add a new shortcut:
  - Command: xfce4-popup-clipman
  - Shortcut: Assign a key combination (e.g., Ctrl + Shift + V or any preferred combination).

_For startup applications, you can add Clipman to automatically start with your system:_

```bash
xfce4-session-settings
```

- Go to the Application Autostart Tab
- Click on the "Application Autostart" tab.
  Add Clipman to Autostart
  - Click the "Add" button. Fill in the fields as follows:
    - Name: Clipman
    - Command: xfce4-clipman
    - Description: Clipboard Manager
    - Click OK.
  - Verify the Entry
    - Ensure the Clipman entry is checked (enabled) in the list.
  - Test the Configuration
    - Restart your PC to confirm Clipman starts automatically. After logging in, you should see the Clipman icon in your system tray.

**31. Droidcam setup**

Droidcam installation [official step](https://www.dev47apps.com/droidcam/linux/)

```bash
wget -O droidcam_latest.zip https://files.dev47apps.net/linux/droidcam_2.1.3.zip
unzip droidcam_latest.zip -d droidcam
cd droidcam && sudo ./install-client
```

for fixing video loopback issue

```bash
sudo apt update
sudo apt install v4l2loopback-dkms
sudo modprobe v4l2loopback
ls /dev/video*
```

_You should see devices like /dev/video0 or /dev/video1._

Ensure the video group has access. If not, add your user to the video group:

```bash
sudo usermod -aG video $USER
```

remove and reload the v4l2loopback module:

```bash
sudo modprobe -r v4l2loopback
sudo modprobe v4l2loopback devices=1 exclusive_caps=1
ls /dev/video*
```

```bash
sudo usermod -aG video $USER
```

restart system then open droidcam in mobile and pc then connect. The ensure you have proper permission on browser level.

**_For usb connection install adb_**

```bash
sudo apt update
sudo apt install adb -y
adb version
```

for allow in phone run this command, you must enable developer option in phone and usb debugging

```bash
adb devices
```

**32. Install OBS**

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install obs-studio
```

_For HD Recording_

```bash
sudo apt install ffmpeg
```

_For NVIDIA GPU accelaeration If you have GPU_

```bash
sudo apt install vainfo i965-va-driver
sudo apt install nvidia-driver-<version>
sudo apt install libnvenc
```

**33. Install NoiseTorch For AI Noice Cancellation**

Download software from [GitHub](https://github.com/noisetorch/NoiseTorch/releases)

```bash
tar -xzf filename.tar.gz
or
tar -xvzf filename.tgz

```

```bash
sudo apt update
sudo apt install pulseaudio
```

_Find file path and goto open terminal and change file ownership_

```bash
sudo chown yourusername:yourusername noisetorch
```

```bash
chmod +x noisetorch
./noisetorch
```

_For global noisetorch execution_

```bash
# create a folder noisetorch inside /home/username/.local/share
# then your noisetorch file that you found when you unzip it. all files keep in .local, may be
# you need on hidden files to see it
# then move bin and other file move in /home/username/.local/share/noisetorch folder
```

```bash
nano ~/.bashrc
```

```bash
export PATH=$PATH:/home/username/.local/share/noisetorch/bin
# save and exit
```

```bash
source ~/.bashrc
echo $PATH
source ~/.bashrc
```

now you can run noisetorch from anywhere

```bash
noisetorch
```

**34. Create multile sshkey for multiple github**

```bash
ssh-keygen -t rsa -b 4096 -C "secondaccount@example.com" -f ~/.ssh/id_rsa_second_account
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa_second_account
cat ~/.ssh/id_rsa_second_account.pub
```

add this key to github account

```bash
cd ~/.ssh
nano config
```

add this configuration

```bash
# Default (Main GitHub account)
Host github.com
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa

# Second GitHub account
Host github-second
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_second_account
```

check configuration

```bash
cat ~/.ssh/config
```

lastly

```bash
# Start the SSH agent
eval "$(ssh-agent -s)"

# Add your main key here rsa replace with your .pub file name
ssh-add ~/.ssh/id_rsa

# Add your second key
ssh-add ~/.ssh/id_rsa_second_account
```
