---
title: Raspberry Pi 4
description: Raspberry Pi 4 部署说明
published: true
date: 2020-04-13T02:09:21.111Z
tags: 
---

![](https://lx-public-pic.oss-cn-shanghai.aliyuncs.com/PicGo/20191205103453.gif)

# k3s

[Five years of Raspberry Pi Clusters](https://medium.com/@alexellisuk/five-years-of-raspberry-pi-clusters-77e56e547875)

# Official (based on Debian)

```bash
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
sudo cp /etc/apt/sources.list.d/raspi.list /etc/apt/sources.list.d/raspi.list.bak

cat << EOF > sources.list
deb http://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/ buster main contrib non-free rpi
deb-src http://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/ buster main contrib non-free rpi
EOF

cat << EOF > raspi.list
deb http://mirrors.tuna.tsinghua.edu.cn/raspberrypi/ buster main ui
deb-src http://mirrors.tuna.tsinghua.edu.cn/raspberrypi/ buster main ui
EOF

mkdir -p ~/.pip/
cat << EOF > ~/.pip/pip.conf
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple/
EOF

sudo cp sources.list /etc/apt/sources.list
sudo cp raspi.list /etc/apt/sources.list.d/raspi.list

sudo apt update
sudo apt upgrade -y

sudo apt install -y git vim htop ncdu tmux bash-completion

# sudo apt install -y zsh zsh-autosuggestions zsh-syntax-highlighting zsh-theme-powerlevel9k remmina remmina-common remmina-dev remmina-plugin-rdp remmina-plugin-vnc fcitx fcitx-googlepinyin fcitx-module-cloudpinyin fcitx-sunpinyin
# cat << EOF > ~/.zshrc
# source /usr/share/powerlevel9k/powerlevel9k.zsh-theme
# source /usr/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
# source /usr/share/zsh-autosuggestions/zsh-autosuggestions.zsh

# export TERM="xterm-256color"

# POWERLEVEL9K_PROMPT_ON_NEWLINE=true
# POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(os_icon user dir_writable dir vcs)
# POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=(status command_execution_time root_indicator background_jobs time disk_usage ram load)
# POWERLEVEL9K_MULTILINE_LAST_PROMPT_PREFIX="%(?:%{$fg_bold[green]%}➜ :%{$fg_bold[red]%}➜ )"
# POWERLEVEL9K_MULTILINE_FIRST_PROMPT_PREFIX=""
# POWERLEVEL9K_USER_ICON="\uF415" # <U+F415>
# POWERLEVEL9K_ROOT_ICON="\uF09C"
# POWERLEVEL9K_SUDO_ICON=$'\uF09C' # <U+F09C>
# POWERLEVEL9K_TIME_FORMAT="%D{%H:%M}"
# POWERLEVEL9K_VCS_GIT_ICON='\uF408'
# POWERLEVEL9K_VCS_GIT_GITHUB_ICON='\uF408'
# EOF

echo 'You can now reboot your rpi to take effect, Good Luck!'
```

## Install Docker

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh  --mirror Aliyun
mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors":["https://docker.mirrors.ustc.edu.cn"]
} 
EOF
sudo systemctl enable docker
sudo systemctl daemon-reload
sudo systemctl start docker
# sudo systemctl restart docker
sudo docker version
```

## Install Docker Compose

```bash
sudo apt install -y libssl-dev libffi-dev
sudo apt install -y python3-pip
pip3 install docker-compose
```

## Raspbian Buster Lite

Default user: pi
Default user password: raspberry

Turn on SSH:

`sudo raspi-config`, choose `5 Interface Options`, then choose `SSH` to enable.

Connect WiFi:

`sudo raspi-config`, choose `2 Network Options`, then choose `N2 Wi-fi` and enter SSID & password to connect.

# Manjaro For ARM

## Download system file

Download system installation mirror files at [OSDN](https://osdn.net/projects/manjaro-arm/storage/rpi4/), you can choose form minimal, xfce, kde-plasma, mate and lxqt.

## Flash to TF card

Use [Etcher](https://www.balena.io/etcher/) or `dd` command described below:

1. find portable device in Mac OS (use `diskutil list`) or Linux (use `lsblk` or `df` or something), for example `/dev/disk2`.
2. Unmount portable device on Mac OS (`diskutil unmountDisk /dev/disk2`) or Linux (`umount /dev/sdb`).
3. Use command `dd` to flash a system file to portable device like below:

```bash
sudo dd if=path/to/img_or_iso of=/dev/disk2 bs=4m;sync
```

> Remember to eject the portable device after above steps on Mac OS (`diskutil eject /dev/disk2`) or Linux (`eject -s /dev/disk2`).

## Choose mirror

> For users in China, Denmark is the fastest mirror currently.

```bash
sudo pacman-mirrors -c Denmark -m rank [-i]
```

## Instalation Script

```bash
sudo cp /etc/pacman.conf /etc/pacman.conf.bak

cat << EOF > ~/pacman.conf
[options]
HoldPkg      = pacman glibc manjaro-system
XferCommand = /usr/bin/curl -x http://192.168.120.63:8888 -C - -f %u --output %o
Architecture = aarch64

CheckSpace
VerbosePkgLists

SigLevel    = Required DatabaseOptional
LocalFileSigLevel = Optional

[core]
Include = /etc/pacman.d/mirrorlist

[extra]
Include = /etc/pacman.d/mirrorlist

[community]
Include = /etc/pacman.d/mirrorlist

EOF

sudo cp ~/pacman.conf /etc/pacman.conf

git config --global http.proxy http://192.168.120.63:8888
git config --global https.proxy http://192.168.120.63:8888
export http_proxy="http://192.168.120.63:8888"; export https_proxy="http://192.168.120.63:8888"; export ftp_proxy="http://192.168.120.63:8888"

sudo pacman-mirrors -c United_States -m rank
sudo pacman -Syyu
sudo pacman -S patch pkgconf fakeroot autoconf automake make cmake gcc clang vim yay wqy-microhei binutils nasm
yay -S xrdp
sudo systemctl enable xrdp.service
sudo systemctl start xrdp.service
sudo pacman -S remmina
# sudo pacman -S patch pkgconf fakeroot autoconf automake make cmake gcc clang vim yay wqy-microhei freerdp remmina
# yay -S xrdp xorgxrdp remmina-plugin-rdesktop remmina
# libtool --finish /usr/lib/xrdp
# libtool --finish /usr/lib/xorg/modules/input
```

# Windows IoT For ARM

## Download system

Go to [UUP dump](https://uupdump.ml/), choose a system version (arm64), and choose `Download using aria2 and convert`, get the generated `*.zip` file, extract it, then run `*.cmd` under a windows system, you will get the `*.iso` system mirror file.

## Deploy system to TF card

First, download [WOA](https://github.com/WOA-Project/WOA-Deployer-Rpi).

Then, open system file (`*.iso`), and choose `source/install.wim` as source for deploying.

# Software

## Aria2 & NG

```bash
git clone git@github.com:NTLx/aira2-ng.git
docker build -t aira2webui-ng aira2-ng
docker run -d --name='aria2' -p '6800:6800/tcp' -p '6800:6800/udp' -p '8888:80/tcp' -p '8888:80/udp' -v '/home/pi/Download':'/data':'rw' -v '/home/pi/aria2_conf':'/config':'rw' aira2webui-ng
```