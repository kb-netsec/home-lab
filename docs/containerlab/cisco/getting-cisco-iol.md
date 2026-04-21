This was a bit of a pain, but in a nutshell:

Download CML free refplat

Unzip and mount the .iso

Clone vrnetlab. The srl-labs fork, not the upstream (https://github.com/srl-labs/vrnetlab.git)

Copy iol binaries to vrnetlab/cisco/iol 

```
$ cp /mnt/CML/virl-base-images/ioll2-xe-17-16-01a/x86_64_crb_linux_l2-adventerprisek9-ms.iol ~/vrnetlab/cisco/iol/
$ cp /mnt/CML/virl-base-images/iol-xe-17-16-01a/x86_64_crb_linux-adventerprisek9-ms.iol ~/vrnetlab/cisco/iol/
```


Create docker containers from iol images
