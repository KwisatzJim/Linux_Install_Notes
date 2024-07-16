### Install Kubuntu for linux gaming

Get kubuntu from ubuntu.com
Burn to flash drive
Install as normal

Setup Ubuntu Pro:

```
sudo pro attach C12v6QKHhWCTvN9sLL5xcWDJ9L3beX
```

```
sudo apt update && sudo apt upgrade -y
```

Install Brave browser:

```

sudo apt install curl
sudo curl -fsSLo /usr/share/keyrings/brave-browser-archive-keyring.gpg https://brave-browser-apt-release.s3.brave.com/brave-browser-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/brave-browser-archive-keyring.gpg] https://brave-browser-apt-release.s3.brave.com/ stable main"|sudo tee /etc/apt/sources.list.d/brave-browser-release.list
sudo apt install brave-browser
```

Install unsnap:
git clone https://github.com/popey/unsnap
cd unsnap/
./unsnap
cd log-XXXXXXXXX/
Do all the scripts

sudo apt install devel-essentials

Install CoreCTRL:

```
sudo add-apt-repository ppa:ernstp/mesarc 
sudo vi /etc/apt/preferences.d/corectrl 
sudo apt install corectrl
```

Install Steam:

```
wget -O ~/steam.deb https://cdn.cloudflare.steamstatic.com/client/installer/steam.deb
sudo dpkg -i ~/steam.deb
steam 
```

Install SteamVR with headset attached Install games

```
Install Flatpak support:
sudo apt install plasma-discover-backend-flatpak
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

Enable ssh:
ssh-keygen
sudo apt install ssh
sudo systemctl enable --now ssh

Enable ufw:
sudo -i
systemctl enable --now ufw
ufw default deny
ufw allow from 10.0.1.0/24
ufw limit ssh
ufw enable
ufw status

