Found a wireless adapter for my Debian lab workstation. I wanted an adapter that had good Linux compatibility with monitor mode and packet injection. 

I plugged it in out of the box and Debian could already see it. Ok, off to a good start. 

```
$ lsusb
Bus 001 Device 063: ID 0e8d:7612 MediaTek Inc. MT7612U 802.11a/b/g/n/ac Wireless Adapter
```

Next I went to https://info.alfa.com.tw/awus036acm 

Went to the Linux support page which had an adorable support table. I've added my own headers here for amusement and also because theirs didn't have any. 

| OS     | Status     | Is it good?
| -------| ---------- | ------------- |
| Kali 2022.2 | Works out-of-the-box | Good |
| Kali 2021.3 | Works out-of-the-box | Good |
| Ubuntu 22.04 | Works out-of-the-box | Good |
| Ubuntu 20.10 | Works out-of-the-box | Good |
| Debian 11.0.3 | Works | Good |
| Debian 10.7.0 | Works | Good |
| Raspberry Pi OS (32-bit) (rev 2020-08-20) | Works out-of-the-box | Good |
| Raspberry Pi OS (32-bit) (rev 2022-04-04) | Works out-of-the-box | Good |

It says Debian works... I guess that's a good sign at least. I roll my sleeves up and prepare to fiddle with it. Here in 2026 I'm on Debian 13 as of the time of this writing. I know this is an old adapter. I specifically went with an AC adapter as AX adapters didn't have the chipset and/or Linux support I'm looking for. 

Under the Debian section, we have only two steps. 

step 1: Add non-free APT source

Append following configuration to the file /etc/apt/sources.list or a file under /etc/apt/sources.list.d/

```
deb http://deb.debian.org/debian/ bullseye non-free
```
Note : Replace bullseye to your system's code name

I've already enabled non-free as part of installing Steam on my (lab lol) workstation. 

```
# Verify non-free APT source added
$cat /etc/apt/sources.list.d/*.sources
Components: main contrib non-free non-free-firmware
```

step 2: Run commands to install firmware

sudo apt update
sudo apt install firmware-misc-nonfree

Looks like I don't have firmware-misc-nonfree. I install it. 

Do I have a wireless interface?

```
ip a
 ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: eno1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether dc:4a:3e:9a:26:13 brd ff:ff:ff:ff:ff:ff
    altname enp0s31f6
    altname enxdc4a3e9a2613
    inet 192.168.88.243/24 brd 192.168.88.255 scope global dynamic noprefixroute eno1
       valid_lft 1469sec preferred_lft 1469sec
    inet6 fe80::de4a:3eff:fe9a:2613/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
3: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default 
    link/ether 02:16:bb:64:a5:4e brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
       valid_lft forever preferred_lft forever
```

Nope. 







