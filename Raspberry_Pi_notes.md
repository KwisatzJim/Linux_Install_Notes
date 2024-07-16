### Raspberry Pi notes

**to edit the EEPROM configuration:**

```
sudo -E rpi-eeprom-config --edit
```

| **BOOT_ORDER** | **Description**                                                                    |
|------------|--------------------------------------------------------------------------------|
| 0xf14      | Try SD first, followed by USB-MSD then repeat (default if BOOT_ORDER is empty) |
| 0xf41      | Try USB first, followed by SD then repeat                                      |
| 0xf21      | Try SD first, followed by NETWORK then repeat                                  |

**for ubuntu server:**

```
sudo apt install bat ipcalc nmap btop gpm iperf3 mtr neofetch shellcheck git bind9 zsh speedtest-cli raspi-config
```

**Setup online backups:**

```
git clone https://github.com/billw2/rpi-clone.gitcd rpi-clonesudo cp rpi-clone rpi-clone-setup /usr/local/sbin
```

**install oh-my-zsh**

```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

**to get ethernet working:**

\[examples in /usr/share/doc/netplan/examples/‘

```
sudo vi /etc/netplan/50-dhcp.yaml
```

```
network:
	version: 2
	renderer: networkd
	ethernets:
		eth0:
			dhcp4: true
```

**Fix display issues:**

```
sudo vi /boot/firmware/config.txt
```

```
display_auto_detect=1
dtoverlay=vc4-fkms-v3d
```
