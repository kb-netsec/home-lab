I wanted to play around with an NMS to better understand SNMP in my homelab. After some googling, the consensus is that LibreNMS is the best all-rounder for home labbers. Zabbix later if I want to go down a rabbit hole, but I'm looking for a quick win for now. 

Ok, let's start with the source. docs.librenms.org/

Some quick google-fu says docker is best as otherwise I'll bungle it due to complex dependency configurations (mariadb, redis, etc.)

First I'll verify docker is installed:

```
docker --version
Docker version 29.6.1, build 8900f1d
```

Looks good. 

Docker quickstart says to download and unzip composer files:

```
mkdir librenms
cd librenms
wget https://github.com/librenms/docker/archive/refs/heads/master.zip
unzip master.zip
cd docker-master/examples/compose
```
Then to "Set a new mysql password in .env and inspect compose.yml"

Uhhh what? How do I set a password in .env? What even does "inspect compose.yml" mean? Inspect it for what? 

At this point, I'm already reaching for a YT tutorial for noobs. I found one by for day in life: that explained the dependencies pretty well.

<iframe width="560" height="315" src="https://www.youtube.com/embed/tQ2pZkk4Fsw?si=_tc2Sykntvbk0ef7" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>







