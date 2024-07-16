### Install Manjaro Linux with KDE

boot to Manjaro usb

start installer

Install it yo

Reboot, login, install updates, reboot

additional packages to install

vim bat bat-extras ipcalc nmap btop iperf3 mtr shellcheck base-devel bind ufw ufw-extras bitwarden signal-desktop tailscale fprint thunderbird tlp cups easyeffects flatpak linux-firmware-qlogic iio-sensor-proxy brave needrestart krdc

create softlink for vim

ln -s /usr/bin/vim /usr/bin/vi

edit pacman.conf

vi /etc/pacman.conf  
uncomment color  
uncomment parallel downloads

change shell to zsh

```bash
chsh -s `which zsh`
```

chsh

/usr/bin/zsh

setup zsh

prepare command-not-found

sudo pkgfile -u

sudo systemctl enable pkgfile-update.timer

sudo systemctl start pkgfile-update.timer

Enable tailscale

sudo systemctl enable tailscaled

sudo systemctl start tailscaled

enable tlp

sudo systemctl enable tlp.service

enable sshd

sudo systemctl enable sshd

sudo systemctl start sshd

ssh-keygen

ssh-copy-id -i .ssh/id_rsa.pub USERNAME@10.0.1.8

ssh dar

cd \~/Library/Mobile\\ Documents/com\~apple\~CloudDocs/Downloads

scp config USERNAME@10.0.1.144:/home/USERNAME/.ssh/

Enable cups

sudo systemctl enable cups

sudo systemctl enable cups

open Settings and set autolaunch for yakuake

set dark mode

install espanso-wayland from aur

espanso service register

espanso start

copy the config entries from bitwarden to the config file thingy

espanso edit

Install missing firmware

aic94xx-firmware wd719x-firmware

Setup sync in Brave

start tailscale

sudo tailscale up

setup fingerprint login

go into settings > user and set it up  
then edit the file to make sudo work with fingerprint on the command line  
sudo vi /etc/pam.d/sudo  
edit the line auth to:  
auth sufficient pam_fprintd.so

/etc/pam.d/sddm

auth 			\[success=1 new_authtok_reqd=1 default=ignore\]  	pam_unix.so try_first_pass likeauth nullok

auth 			sufficient  	pam_fprintd.so

/etc/pam.d/kde

auth 			sufficient  	pam_unix.so try_first_pass likeauth nullok

auth 			sufficient  	pam_fprintd.so

setup ufw

sudo -i

systemctl enable ufw

systemctl start ufw

ufw default deny

ufw allow from 10.0.1.0/24

ufw allow from 100.64.0.0/10

ufw limit ssh

ufw enable

cntrl-d

Setup ssh

ssh-keygen

Connect WiFi if using wired so far

Setup Thunderbird and import pgp keys

add Framework specific kernel parameters

sudo pacman -Syyu --noconfirm && sudo sed -i.bak 's/^\\(GRUB_CMDLINE_LINUX_DEFAULT="\[^"\]\*\\)"$/\\1 module_blacklist=hid_sensor_hub nvme.noacpi=1"/' /etc/default/grub && sudo update-grub && echo "\[connection\]" | sudo tee /etc/NetworkManager/conf.d/default-wifi-powersave-on.conf && echo "wifi.powersave = 2" | sudo tee -a /etc/NetworkManager/conf.d/default-wifi-powersave-on.conf && sleep 1 && sudo echo -e "\\033\[1;33mProcess is complete"
