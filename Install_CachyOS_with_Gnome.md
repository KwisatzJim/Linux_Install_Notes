### Install CachyOS with Gnome

boot to CachyOS usb

start installer

set options and choose Gnome desktop

begin install

reboot

login

create softlink for vim

```
sudo rm /usr/bin/vi 
sudo ln -s /usr/bin/vim /usr/bin/vi
```

prepare command-not-found

```
sudo pkgfile -u
sudo systemctl enable --now pkgfile-update.timer
```

install Chaotic:

- First, install the primary key - it can then be used to install our keyring and mirrorlist: 
  - pacman-key --recv-key 3056513887B78AEB --keyserver keyserver.ubuntu.com
  - pacman-key --lsign-key 3056513887B78AEB
  - pacman -U 'https://cdn-mirror.chaotic.cx/chaotic-aur/chaotic-keyring.pkg.tar.zst' 'https://cdn-mirror.chaotic.cx/chaotic-aur/chaotic-mirrorlist.pkg.tar.zst'
- Append (adding to the end of the file) to /etc/pacman.conf: 
  - \[chaotic-aur\]
  - Include = /etc/pacman.d/chaotic-mirrorlist
- Install with CachyOS Package Manager: signal-desktop thunderbird pamac
- Install with Pamac: unarchiver bat-extras ipcalc nmap iperf3 mtr shellcheck ufw bitwarden tailscale fprint tlp tlp-ui easyeffects linux-firmware-qlogic iio-sensor-proxy needrestart espanso-wayland aic94xx-firmware wd719x-firmware upd72020x-fw rpi-imager renamemytvseries-qt-bin protonvpn extension-manager

Then install Search Light and auto-move windows and set signal, thunderbird, and firefox to desired workspace.

Enable tailscale

```
sudo systemctl enable --now tailscaled
```

enable tlp

```
sudo systemctl enable --now tlp.service
```

enable sshd

```
sudo systemctl enable --now sshd
```

open Settings and launch guake

setup f12 to work

in settings for keyboard set customer shortcut for guake-toggle

add the following line to \~/.config/fish/config.fish

```
source /usr/share/doc/pkgfile/command-not-found.fish
```

```
source ~/.config/fish/config.fish
```

set dark mode

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

setup ufw

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

Setup ssh key

```
ssh-keygen
```

Connect WiFi if using wired so far

Setup Thunderbird and import pgp keys, setup contacts before calendars so as to avoid the weirdness with nextcloud calendars

add Framework specific kernel parameters

```
sudo vi /boot/loader/entries/XXXXXXXX_linux.conf
```

```
nvme.noacpi=1
```

configure tlp

```
sudo vi /etc/tlp.d/01-custom.conf
```

```
CPU_SCALING_GOVER
NOR_ON_AC=powersave 
CPU_SCALING_GOVERNOR_ON_BAT=powersave
CPU_BOOST_ON_AC=0
CPU_BOOST_ON_BAT=0
PCIE_ASPM_ON_BAT=powersupersave
PLATFORM_PROFILE_ON_AC=balanced
PLATFORM_PROFILE_ON_BAT=low-power
USB_ALLOWLIST=32ac:0002
USB_EXCLUDE_BTUSB=1
USB_EXCLUDE_PRINTER=0
WIFI_PWR_ON_AC=off
WIFI_PWR_ON_BAT=off
WOL_DISABLE=N
```

```
sudo systemctl restart tlp
```

setup some audio stuff

```
for u in pipewire.socket pipewire-pulse.socket; do systemctl enable --now --user $u; done
```

logout and login
