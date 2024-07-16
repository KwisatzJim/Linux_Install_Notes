### Archinstall notes

List of additional packages to install for all:

base-devel  
easyeffects  
fastfetch  
firefox  
fish  
flatpak  
fprint  
git  
handbrake  
iio-sensor-proxy  
intel-ucode  
ipcalc  
iperf3  
linux-firmware-qlogic  
man-db  
man-pages  
mtr  
nano  
nextcloud-client  
nmap  
pkgfile  
qbittorrent  
shellcheck  
signal-desktop  
tailscale  
texinfo  
thunderbird  
tlp  
ufw  
unarchiver  
usbutils  
vim  
vlc  
wget

list of additional packages to install for Gnome:  
guake  
gufw

list of additional packages to install for KDE:  
dolphin-plugins  
ffmpegthumbs  
kde-utilities-meta  
kdegraphics-thumbnailers  
kde-system-meta  
kio-admin  
kio-extras  
kio-fuse  
print-manager  
xwaylandvideobridge  
yakuake

can add Chaotic-aur and install the following instead of going through yay:
aic94xx-firmware  
ast-firmware  
balena-etcher  
pamac-aur  
plex-media-player  
protonvpn-cli  
protonvpn-gui  
qownnotes  
rpi-imager  
tlpui  
trizen  
upd72020x-fw  
wd719x-firmware  
yay  
zoom

install Chaotic:

- First, install the primary key - it can then be used to install our keyring and mirrorlist: 
  - pacman-key --recv-key 3056513887B78AEB --keyserver keyserver.ubuntu.com
  - pacman-key --lsign-key 3056513887B78AEB
  - pacman -U 'https://cdn-mirror.chaotic.cx/chaotic-aur/chaotic-keyring.pkg.tar.zst' 'https://cdn-mirror.chaotic.cx/chaotic-aur/chaotic-mirrorlist.pkg.tar.zst'
- Append (adding to the end of the file) to /etc/pacman.conf: 
  - \[chaotic-aur\]
  - Include = /etc/pacman.d/chaotic-mirrorlist

list of additional packages to install with yay or yup:  
needrestart  
espanso-wayland  
renamemytvseries-qt-bin

establish wifi on arch linux install disk
iwctl
station wlan0 scan
station wlan0 get-networks
station wlan0 connect ’Nuit 5GHz’

fix broken encryption in archinstall:
pacman -Sy archinstall
