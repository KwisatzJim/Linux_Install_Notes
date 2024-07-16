### Resize LVM drive in linux

```
sudo lvextend -l +100%FREE /dev/mapper/ubuntu--vg-ubuntu--lv
```

```
sudo resize2fs /dev/mapper/ubuntu--vg-ubuntu--lv
```

May need to do these:

```
sudo growpart /dev/sdc 3
```

```
sudo e2fsck -f /dev/sdc3
```

```
sudo resize2fs /dev/sdc 3
```
