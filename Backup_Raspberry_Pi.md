### Backup Raspberry Pi

- You’ll need to install Git to download the files:

```
sudo apt-get install git
```

- Start by downloading and installing the script:

```
cd ~/Downloads
git clone https://github.com/billw2/rpi-clone.git  
cd rpi-clonesudo 
cp rpi-clone rpi-clone-setup /usr/local/sbin
```

- Then use fdisk to get the backup SD card name:

```
sudo fdisk -l
```

You should see the current SD card: sda or mmcblk0 most of the time.

- And below the backup SD card: sdb or mmcblk1 generally
- And finally, use rpi-clone:

```
sudo rpi-clone sdb -v
```

Replace sdb with your backup SD card name.

**For my Pi:**

```
sudo rpi-clone sda -v -F
```

**To restore from backup:**

- Insert backup SD card
- Reboot so that it boots from SD card
- Run:   
```
  sudo rip-clone mmcblk0 -v -F
```
