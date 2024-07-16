### Install Arch LInux for making ALCI

boot to arch usb

edit pacman.conf

```
vi /etc/pacman.conf
```

```
uncomment color
uncomment parallel downloads
Add ILoveCandy
```

start installer

```
archinstall
```

set options and choose Server or Minimal

additional packages to install

vim nano wget bat bat-extras neofetch man-db man-pages intel-ucode base-devel git pkgfile zsh usbutils linux-firmware-qlogic iio-sensor-proxy archiso

begin install

chroot and do the following:

create softlink for vim

```
ln -s /usr/bin/vim /usr/bin/vi
```

edit pacman.conf

```
vi /etc/pacman.conf
```

```
uncomment color
uncomment parallel downloads
```

change shell to zsh

chsh -s which zsh USERNAME

su - USERNAME

setup zsh

prepare command-not-found

```
pkgfile -u
```

```
systemctl enable pkgfile-update.timer
```

enable sshd

```
systemctl enable sshd
```

exit chroot

reboot

login

install oh-my-zsh

```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

change .zshrc to prefered stuff

set theme to steeef

add the following line to .zshrc

```
source /usr/share/doc/pkgfile/command-not-found.zsh
```

```
source .zshrc
```

Install yay

```
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
```

Packages to install with yay:

needrestart, aic94xx-firmware, wd719x-firmware, upd72020x-fw

Setup ssh key

```
ssh-keygen
```

