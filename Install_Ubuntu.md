### Install Ubuntu

download iso from here:

https://ubuntu.com/download/desktop

burn onto usb drive with Balena Etcher

boot to it

run through the installer, it's easy

reboot into newly installed OS

additional packages to install

vim wget btop iperf3 neofetch ufw  command-not-found zsh zsh-common git curl guake needrestart needrestart-session ffmpeg intel-gpu-tools

Install Flatpak and EasyEffects

```
sudo apt install flatpak
sudo add-apt-repository ppa:flatpak/stable
sudo apt update
sudo apt install flatpak
sudo apt install gnome-software-plugin-flatpak
```

flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo

```
sudo reboot
```

```
flatpak install flathub com.github.wwmm.easyeffects
```

Install Bitwarden

```
sudo snap install bitwarden
```

change shell to zsh

```
chsh -s `which zsh`
```

```
su jim
```

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

```
sh -c "$(curl -fsSL <https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh>)"
```

change .zshrc to preferred stuff

set theme to steeef
add the following line to .zshrc

```
source /usr/share/doc/pkgfile/command-not-found.zsh
```

```
source .zshrc
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

setup fingerprint authentication

go into settings -> users and setup fingerprint

in terminal:

```
sudo pam-auth-update
```

Install tailscale

```
curl -fsSL <https://tailscale.com/install.sh> | sh
```

```
sudo tailscale up
```

Setup Thunderbird and import pgp keys, setup contacts before calendars so as to avoid the weirdness with nextcloud calendars

add some framework fixes

```
sudo apt update && sudo apt upgrade -y && sudo snap refresh && echo "options snd-hda-intel model=dell-headset-multi" | sudo tee -a /etc/modprobe.d/alsa-base.conf && gsettings set org.gnome.mutter experimental-features "['scale-monitor-framebuffer']" && sudo sed -i 's/^GRUB_CMDLINE_LINUX_DEFAULT.*/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash module_blacklist=hid_sensor_hub nvme.noacpi=1"/g' /etc/default/grub && sudo update-grub && echo "[connection]" | sudo tee /etc/NetworkManager/conf.d/default-wifi-powersave-on.conf && echo "wifi.powersave = 2" | sudo tee -a /etc/NetworkManager/conf.d/default-wifi-powersave-on.conf
```

```
sudo vi /etc/default/console-setup
```

set FONTSIZE=32x16 and FONTFACE="Terminus".

```
sudo vi /etc/default/grub
```

set GRUB_GFXMODE=1024x768

```
sudo update-grub
```

```
sudo reboot
```

Setup ssh config

download the config file from Nextcloud and put it in \~/.ssh

ssh-copy-id -i .ssh/id_rsa.pub jimkelley@10.0.1.8ssh-copy-id -i .ssh/id_rsa.pub jimkelley@10.0.1.209ssh-copy-id -i .ssh/id_rsa.pub jimkelley@10.0.1.14ssh-copy-id -i .ssh/id_rsa.pub jimkelley@10.0.1.91ssh-copy-id -i .ssh/id_rsa.pub jim@10.0.1.142ssh-copy-id -i .ssh/id_rsa.pub jim@10.0.1.141ssh-copy-id -i .ssh/id_rsa.pub neon@10.0.1.59

Install espanso

```
curl --proto '=https' --tlsv1.2 -sSf <https://sh.rustup.rs> | sh
```

```
source "$HOME/.cargo/env"
```

```
sudo apt update && sudo apt install build-essential git wl-clipboard libxkbcommon-dev libdbus-1-dev libssl-dev
```

```
cargo install --force cargo-make --version 0.34.0
```

```
git clone <https://github.com/federico-terzi/espanso>

cd espanso

cargo make --profile release --env NO_X11=true build-binary

sudo mv target/release/espanso /usr/local/bin/espanso

sudo setcap "cap_dac_override+p" $(which espanso)

espanso service register

espanso start
```

```
espanso edit
```

add the config stuff saved in bitwarded under espanso

```
espanso install basic-emojis
```

```
espanso install apple-symbols
```

```
cd ..
```

```
rm -rf espanso
```

Install Signal Desktop

```
sudo apt install dirmngr ca-certificates software-properties-common apt-transport-https curl -y

curl -fsSL <https://updates.signal.org/desktop/apt/keys.asc> | gpg --dearmor | sudo tee /usr/share/keyrings/signal-desktop-keyring.gpg > /dev/null

echo "deb [arch=amd64 signed-by=/usr/share/keyrings/signal-desktop-keyring.gpg] <https://updates.signal.org/desktop/apt> xenial main" | sudo tee /etc/apt/sources.list.d/signal-messenger.list

sudo apt update

sudo apt install signal-desktop -y
```

Setup EasyEffect presets:

```
git clone <https://github.com/ceiphr/ee-framework-presets>
```

open EasyEffects and import the presets

Install the Gnome Extensions Manager

```
sudo apt install gnome-shell-extension-manager
```

Then install Search Light and auto-move windows and set signal, Thunderbird, and Firefox to desired workspace.

Set hardware video acceleration in Firefox

```
about:config
```

media.ffmpeg.vaapi.enabled = true

media.rdd-ffmpeg.enabled = true
