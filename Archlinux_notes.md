### Arch linux notes

Update all packages on Arch Linux

sudo pacman -Syu

Update all packages and fix any corruption

sudo pacman -Syyu

Update specific package

sudo pacman -S package_name

Quiry packages

sudo pacman -Ss package_name

Get info about a package

sudo pacman -Si package_name

Remove packages

sudo pacman -Rs package_name

remove all orphan packages and configuration files for removed apps

sudo pacman -Qtdq | pacman -Rns -

change default shell:

chsh -l

chsh -s <full-path-to-shell>

Install yay

sudo pacman -S --needed base-devel git

git clone https://aur.archlinux.org/yay.git

cd yay

makepkg -si

establish wifi on arch linux install disk

iwctl

station wlan0 scan

station wlan0 get-networks

station wlan0 connect ’Nuit 5GHz’

install dig command

sudo pacman -S bind

get sudo command to do tab completion

in .bashrc add the following line:

complete -cf sudo

to get the command not found to show what package to install

install pkgfile then run:

sudo pkgfile -u

add the following line to .bashrc

source /usr/share/doc/pkgfile/command-not-found.bash

then to enable automatic updates of pkgfile database

sudo systemctl enable pkgfile-update.timer

Clear the screen after logging out

in .bash_logout add the following lines

clear

reset

install an app that checks your shell scripts

yay shellcheck

enable mouse support in terminal

sudo pacman -S gpm

sudo systemctl enable gpm.service

sudo systemctl start gpm.service

enable parallel downloads in pacman

in /etc/pacman.conf in the \[options\] section uncomment the ParallelDownloads option

Restart daemons after library updates

yay needrestart

Change kernel parameters here:

/boot/loader/entries/XXXX.conf
