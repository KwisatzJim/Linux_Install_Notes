### Install Arch Linux with KDE

boot to arch usb \[don't use net installer!\]

edit pacman.conf:

```
vi /etc/pacman.conf
```

uncomment color
uncomment parallel downloads
Add ILoveCandy

Update archinstall:

```
pacman -Sy archinstall
```

start installer:

archinstall

set options and choose KDE desktop

additional packages to install

vim nano wget unarchiver bat bat-extras ipcalc nmap btop iperf3 mtr neofetch shellcheck man-db man-pages texinfo intel-ucode base-devel git bind pkgfile fish yakuake ufw bitwarden signal-desktop tailscale fprint usbutils firefox thunderbird tlp cups easyeffects flatpak linux-firmware-qlogic iio-sensor-proxy handbrake kde-utilities-meta kde-system-meta vlc qbittorrent nextcloud-client dolphin-plugins ffmpegthumbs kdegraphics-thumbnailers kio-admin kio-extras kio-fuse print-manager xwaylandvideobridge

begin install

chroot and do the following:

create softlink for vim:

```
ln -s /usr/bin/vim /usr/bin/vi
```

edit pacman.conf

vi /etc/pacman.conf
uncomment color
uncomment parallel downloads

change shell to fish

```
chsh -s `which fish`
```

```
su USERNAME
```

```
exit
```

prepare command-not-found

```
pkgfile -u
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

open Settings and set autolaunch for yakuake

add the following to .config/fish/config_fish:

```
source /usr/share/doc/pkgfile/command-not-found.fish
```

```
source .config/fish/config_fish
```

set dark mode

Install yay

```
git clone https://aur.archlinux.org/yay.git
```

```
cd yay
```

```
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

start tailscale:

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
auth 			[success=1 new_authtok_reqd=1 default=ignore]  	pam_unix.so try_first_pass likeauth nullok
auth 			sufficient  	pam_fprintd.so
```

/etc/pam.d/kde

```
auth 			sufficient  	pam_unix.so try_first_pass likeauth nullok
auth 			sufficient  	pam_fprintd.so
```

setup ufw:

```
sudo -i

systemctl enable ufw

systemctl start ufw

ufw default deny

ufw allow from 10.0.1.0/24

ufw allow from 100.64.0.0/10

ufw limit ssh

ufw enable

exit
```

Setup ssh:

```
ssh-keygen
```

Connect WiFi if using wired so far

Setup Thunderbird and import pgp keys, setup one account at a time and let it update so as to avoid the weirdness with nextcloud calendars

add Framework specific kernel parameters

```
sudo vi /boot/loader/entries/XXXXXX_linux.conf
```

```
net.ifnames=0 libata.allow_tpm=1 module_blacklist=cros_ec_lpcs,hid_sensor_hub acpi_osi="!Windows 2020" tpm_tis.interrupts=0 nvme.noacpi=1 mem_sleep_default=s2idle
```

configure tlpui per https://knowledgebase.frame.work/en_us/optimizing-ubuntu-battery-life-Sye_48Lg3

setup some audio stuff

```
for u in pipewire.socket pipewire-pulse.socket; do systemctl enable --now --user $u; done
```

Install EasyEffects presets for Framework laptops

```
git clone <https://github.com/ceiphr/ee-framework-presets>
```

open Easy Effects once to create config directory
open Easy Effect and setup preferences in such
