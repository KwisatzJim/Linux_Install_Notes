### Fix for failed to check for processor microcode

sudo vi /etc/needrestart/needrestart.conf

change

```
#$nrconf{ucodehints} = 0;
```

to

```
$nrconf{ucodehints} = 1;
```
