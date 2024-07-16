### Install Pi-Hole on Raspberry Pi

Use Raspberry Pi Imager to write latest Ubuntu to the SD card

Or

Get image from here and write to Pi’s SD card:

https://ubuntu.com/download/raspberry-pi/thank-you?version=20.10&architecture=server-arm64+raspi

```
sudo timedatectl set-timezone America/Chicago
```

```
sudo hostnamectl set-hostname raspberrypi
```

```
sudo vi /etc/hosts
```

```
127.0.0.1 raspberrypi
```

```
curl -sSL https://install.pi-hole.net | bash
```

```
sudo apt install unbound
```

```
sudo vi /etc/unbound/unbound.conf.d/pi-hole.conf
```

```
server:
    # If no logfile is specified, syslog is used
    # logfile: "/var/log/unbound/unbound.log"
    verbosity: 0

    interface: 127.0.0.1
    port: 5335
    do-ip4: yes
    do-udp: yes
    do-tcp: yes

    # May be set to yes if you have IPv6 connectivity
    do-ip6: no

    # You want to leave this to no unless you have *native* IPv6. With 6to4 and
    # Terredo tunnels your web browser should favor IPv4 for the same reasons
    prefer-ip6: no

    # Use this only when you downloaded the list of primary root servers!
    # If you use the default dns-root-data package, unbound will find it automatically
    #root-hints: "/var/lib/unbound/root.hints"

    # Trust glue only if it is within the server's authority
    harden-glue: yes

    # Require DNSSEC data for trust-anchored zones, if such data is absent, the zone becomes BOGUS
    harden-dnssec-stripped: yes

    # Don't use Capitalization randomization as it known to cause DNSSEC issues sometimes
    # see https://discourse.pi-hole.net/t/unbound-stubby-or-dnscrypt-proxy/9378 for further details
    use-caps-for-id: no

    # Reduce EDNS reassembly buffer size.
    # IP fragmentation is unreliable on the Internet today, and can cause
    # transmission failures when large DNS messages are sent via UDP. Even
    # when fragmentation does work, it may not be secure; it is theoretically
    # possible to spoof parts of a fragmented DNS message, without easy
    # detection at the receiving end. Recently, there was an excellent study
    # >>> Defragmenting DNS - Determining the optimal maximum UDP response size for DNS <<<
    # by Axel Koolhaas, and Tjeerd Slokker (https://indico.dns-oarc.net/event/36/contributions/776/)
    # in collaboration with NLnet Labs explored DNS using real world data from the
    # the RIPE Atlas probes and the researchers suggested different values for
    # IPv4 and IPv6 and in different scenarios. They advise that servers should
    # be configured to limit DNS messages sent over UDP to a size that will not
    # trigger fragmentation on typical network links. DNS servers can switch
    # from UDP to TCP when a DNS response is too big to fit in this limited
    # buffer size. This value has also been suggested in DNS Flag Day 2020.
    edns-buffer-size: 1232

    # Perform prefetching of close to expired message cache entries
    # This only applies to domains that have been frequently queried
    prefetch: yes

    # One thread should be sufficient, can be increased on beefy machines. In reality for most users running on small networks or on a single machine, it should be unnecessary to seek performance enhancement by increasing num-threads above 1.
    num-threads: 1

    # Ensure kernel buffer is large enough to not lose messages in traffic spikes
    so-rcvbuf: 1m

    # Ensure privacy of local IP ranges
    private-address: 192.168.0.0/16
    private-address: 169.254.0.0/16
    private-address: 172.16.0.0/12
    private-address: 10.0.0.0/8
    private-address: fd00::/8
    private-address: fe80::/10
```

```
sudo service unbound restart
```

Start your local recursive server and test that it's operational:

```
sudo service unbound restart
dig pi-hole.net @127.0.0.1 -p 5335
```

The first query may be quite slow, but subsequent queries, also to other domains under the same TLD, should be fairly quick.

You should also consider adding

```
edns-packet-max=1232
```

to a config file like /etc/dnsmasq.d/99-edns.conf to signal FTL to adhere to this limit.

### Test validation¶

You can test DNSSEC validation using

```
dig fail01.dnssec.works @127.0.0.1 -p 5335
dig dnssec.works @127.0.0.1 -p 5335
```

The first command should give a status report of SERVFAIL and no IP address. The second should give NOERROR plus an IP address.

Configure Pi-hole¶

Finally, configure Pi-hole to use your recursive DNS server by specifying 127.0.0.1#5335 as the Custom DNS (IPv4)

Add logging to unbound¶

Warning

It's not recommended to increase verbosity for daily use, as unbound logs a lot. But it might be helpful for debugging purposes.

There are five levels of verbosity

```
Level 0 means no verbosity, only errors
Level 1 gives operational information
Level 2 gives  detailed operational  information
Level 3 gives query level information
Level 4 gives  algorithm  level  information
Level 5 logs client identification for cache misses
```

First, specify the log file, human-readable timestamps and the verbosity level in the server part of /etc/unbound/unbound.conf.d/pi-hole.conf:

```
server:
    # If no logfile is specified, syslog is used
    logfile: "/var/log/unbound/unbound.log"
    log-time-ascii: yes
    verbosity: 1
```

Second, create log dir and file, set permissions:

```
sudo mkdir -p /var/log/unbound
sudo touch /var/log/unbound/unbound.log
sudo chown unbound /var/log/unbound/unbound.log
```

On modern Debian/Ubuntu-based Linux systems, you'll also have to add an AppArmor exception for this new file so unbound can write into it.

Create (or edit if existing) the file /etc/apparmor.d/local/usr.sbin.unbound and append

```
/var/log/unbound/unbound.log rw,
```

to the end (make sure this value is the same as above). Then reload AppArmor using

```
sudo apparmor_parser -r /etc/apparmor.d/usr.sbin.unbound
sudo service apparmor restart
```

Lastly, restart unbound:

```
sudo service unbound restart
```

Setup backup:

```
cd ~/Downloads
git clone https://github.com/billw2/rpi-clone.git
cd rpi-clone
sudo cp rpi-clone rpi-clone-setup /usr/local/sbin
```

If you made a backup of previous pihole settings, restore them

