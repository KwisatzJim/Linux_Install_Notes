### Archlinux - fix gpg key errors

```
sudo rm -rf /etc/pacman.d/gnupg
sudo pacman-key --init
sudo pacman-key --populate
sudo pacman -S archlinux-keyring
```
