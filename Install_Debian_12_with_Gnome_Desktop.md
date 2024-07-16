### Install Debian 12 with Gnome

download iso from here:

https://www.debian.org/download

burn onto usb drive with Balena Etcher

boot to it

run through the installer, it's easy

reboot into newly installed OS

add user as sudoer

> su
>
> sudoedit /etc/sudoers
>
> USERNAME ALL=(ALL:ALL) ALL

additional packages to install

vim wget btop iperf3 neofetch ufw fprintd libpam-fprintd command-not-found zsh zsh-common git curl guake thunderbird easyeffects needrestart needrestart-session

change shell to zsh

```bash
chsh -s `which zsh`
```

chsh  
/usr/bin/zsh  
chsh USERNAME  
/usr/bin/zsh

su USERNAME

setup zsh

Change Settings

launch guake-settings and make desired changes

setup f12 to work

in settings for keyboard set customer shortcut for guake-toggle

change Displays scale to 100%

Power -> show battery percentage

Date & Time -> 12 hour clock

Appearance -> dark mode, wallpaper

Open Tweaks and change font scaling to 1.5, add EasyEffects and Signal to Startup Apps, add weekday to Top Bar,

install oh-my-zsh

sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

change .zshrc to preferred stuff

set theme to steeef  
add the following line to .zshrc  
source /usr/share/doc/pkgfile/command-not-found.zsh

source .zshrc

setup ufw

sudo -i

systemctl enable ufw

systemctl start ufw

ufw default deny

ufw allow from 10.0.1.0/24

ufw allow from 100.64.0.0/10

ufw limit ssh

ufw enable

exit

Setup ssh key

ssh-keygen

setup fingerprint authentication

go into settings -> users and setup fingerprint

in terminal: sudo pam-auth-update

Install tailscale

curl -fsSL https://tailscale.com/install.sh | sh

sudo tailscale up

Setup Thunderbird and import pgp keys, setup contacts before calendars so as to avoid the weirdness with nextcloud calendars

add some framework fixes

sudo vi /etc/default/grub

GRUB_CMDLINE_LINUX_DEFAULT="quiet module_blacklist=hid_sensor_hub nvme.noacpi=1"

sudo update-grub

reboot

Install espanso

curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

source "$HOME/.cargo/env"

sudo apt update && sudo apt install build-essential git wl-clipboard libxkbcommon-dev libdbus-1-dev libwxgtk3.2-dev libssl-dev

cargo install --force cargo-make --version 0.34.0

git clone https://github.com/federico-terzi/espanso

cd espanso

cargo make --profile release --env NO_X11=true build-binary

sudo mv target/release/espanso /usr/local/bin/espanso

sudo setcap "cap_dac_override+p" $(which espanso)

espanso service register

espanso start

espanso edit

add the config stuff saved in bitwarded under espanso

espanso install basic-emojis

espanso install apple-symbols

cd ..

rm -rf espanso

Install Signal Desktop

sudo apt install dirmngr ca-certificates software-properties-common apt-transport-https curl -y

curl -fsSL https://updates.signal.org/desktop/apt/keys.asc | gpg --dearmor | sudo tee /usr/share/keyrings/signal-desktop-keyring.gpg > /dev/null

echo "deb \[arch=amd64 signed-by=/usr/share/keyrings/signal-desktop-keyring.gpg\] https://updates.signal.org/desktop/apt xenial main" | sudo tee /etc/apt/sources.list.d/signal-messenger.list

sudo apt update

sudo apt install signal-desktop -y

Setup EasyEffect presets:

git clone https://github.com/ceiphr/ee-framework-presets

open EasyEffects and import the presets

With such a high screen resolution it is very hard to read the small fonts in console. Edit /etc/default/console-setup and set FONTSIZE=32x16 to get a better font size. Also  you may want to try out FONTFACE="Terminus". Grub fonts are also very hard to read, set GRUB_GFXMODE=1024x768 in /etc/default/grub and run update-grub as root to fix that. Reboot to see the changes.

Install the Gnome Extensions Manager

sudo apt install gnome-shell-extension-manager

Then install Search Light and auto-move windows and set signal, thunderbird, and firefox to desired workspace.
