### Install Arch LInux with Gnome Desktop

boot to arch usb

edit pacman.conf

```
vi /etc/pacman.conf
```

uncomment color

uncomment parallel downloads

Add ILoveCandy

start installer

```
archinstall
```

set options and choose Gnome desktop

additional packages to install

vim nano wget unarchiver bat bat-extras ipcalc nmap btop iperf3 mtr neofetch shellcheck man-db man-pages texinfo intel-ucode base-devel git bind pkgfile zsh guake ufw gufw bitwarden signal-desktop tailscale fprint usbutils firefox thunderbird tlp cups easyeffects linux-firmware-qlogic iio-sensor-proxy

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

uncomment color

uncomment parallel downloads

change shell to zsh

```
chsh -s which zsh
```

```
su - USERNAME
```

setup zsh

prepare command-not-found

```
pkgfile -u
```

```
systemctl enable pkgfile-update.timer
```

Enable tailscale

```
systemctl enable tailscaled
```

enable tlp

```
systemctl enable tlp.service
```

enable sshd

```
systemctl enable sshd
```

Enable cups

```
systemctl enable cups
```

exit chroot

reboot

login

open Settings and launch guake

setup f12 to work

in settings for keyboard set customer shortcut for guake-toggle

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

set dark mode

Install yay

```
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
```

Packages to install with yay:

needrestart, espanso-wayland, aic94xx-firmware, wd719x-firmware, upd72020x-fw, balena-etcher, rpi-imager, renamemytvseries-qt-bin, protonvpn

Setup espanso:

```
espanso service register
```

```
espanso start
```

copy the config entries from bitwarden to the config file thingy

espanso edit \[paste config info\]

start tailscale

```
sudo tailscale up
```

setup fingerprint login

go into settings > user and set it up

then edit the file to make sudo work with fingerprint on the command line

```
sudo vi /etc/pam.d/sudo
```

edit the line auth to:

```
auth sufficient pam_fprintd.so
```

/etc/pam.d/sddm

```
auth 			[success=1 new_authtok_reqd=1 default=ignore]  	pam_unix.so try_first_pass likeauth nullok
```

```
auth 			sufficient  	pam_fprintd.so
```

/etc/pam.d/kde

```
auth 			sufficient  	pam_unix.so try_first_pass likeauth nullok
```

```
auth 			sufficient  	pam_fprintd.so
```

setup ufw

```
sudo -i 
```

```
systemctl enable ufw
```

```
systemctl start ufw
```

```
ufw default deny
```

```
ufw allow from 10.0.1.0/24
```

```
ufw allow from 100.64.0.0/10
```

```
ufw limit ssh
```

```
ufw enable
```

exit

Setup ssh key

```
ssh-keygen
```

Connect WiFi if using wired so far

Setup Thunderbird and import pgp keys, setup contacts before calendars so as to avoid the weirdness with nextcloud calendars

add Framework specific kernel parameters

```
sudo vi /boot/loader/entries/XXXXXX.conf
```

```
net.ifnames=0 libata.allow_tpm=1 module_blacklist=cros_ec_lpcs,hid_sensor_hub acpi_osi="!Windows 2020" tpm_tis.interrupts=0 nvme.noacpi=1 mem_sleep_default=s2idle 
```

configure tlp

```
sudo vi /etc/tlp.d/01-custom.conf
```

> CPU_SCALING_GOVERNOR_ON_AC=powersave CPU_SCALING_GOVERNOR_ON_BAT=powersave
>
> CPU_BOOST_ON_AC=0
>
> CPU_BOOST_ON_BAT=0
>
> PCIE_ASPM_ON_BAT=powersupersave
>
> PLATFORM_PROFILE_ON_AC=balanced
>
> PLATFORM_PROFILE_ON_BAT=low-power
>
> USB_ALLOWLIST=32ac:0002
>
> USB_EXCLUDE_BTUSB=1
>
> USB_EXCLUDE_PRINTER=0
>
> WIFI_PWR_ON_AC=off
>
> WIFI_PWR_ON_BAT=off
>
> WOL_DISABLE=N

```
sudo systemctl restart tlp
```

setup some audio stuff

```
for u in pipewire.socket pipewire-pulse.socket; do systemctl enable --now --user $u; done
```

