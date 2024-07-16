### Disable screen blanking on Raspberry Pi

```
sudo /boot/firmware/cmdline.txt
```

add consoleblank=0 to the end so it shows as follows:

console=serial0,115200 multipath=off dwc_otg.lpm_enable=0 console=tty1 root=LABEL=writable rootfstype=ext4 rootwait fixrtc consoleblank=0
