This was a bit of a pain, but in a nutshell:

Download CML free refplat to your machine.

Unzip and mount the .iso 

```
unzip refplat-20260409-free-iso.zip

sudo mkdir /mnt/cml
cd /mtn/cml

sudo mount -o loop refplat-20260409-free.iso /mnt/cml
```

Clone vrnetlab. The srl-labs fork, not the upstream. It took me way too long to find out the upstream didn't have a Cisco directory. See containerlab documentation here https://containerlab.dev/manual/vrnetlab/#vrnetlab (https://github.com/srl-labs/vrnetlab.git)

```
git clone https://github.com/srl-labs/vrnetlab.git
```

Copy iol binaries to vrnetlab/cisco/iol 7/9/2026 UPDATE: According to AI slop, Staring with (CML) 2.10, the Cisco IOS on Linux (IOL) images are no longer provided as standalone .iol files in the reference platform (refplat) ISO. Instead, they are packaged as docker devices within a compressed archive (e.g., iol-xe-17-18-02.tar.gz) containing blob files with SHA256 hash names

To extract the usable IOL binary for use in emulators like GNS3 or Containerlab, you must perform the following steps:

Extract the tar.gz archive from the ISO to a temporary directory. 
Navigate to the blobs directory (blobs/sha256/) and identify the largest file (typically ~287MB). 
Extract the inner POSIX tar archive from that specific blob file.
Locate the .iol binary (e.g., x86_64_crb_linux-adventerprisek9-ms.iol) within the extracted contents. 
For Containerlab users, you can automate this process using tools like refplatinator or by manually cloning the srl-labs/vrnetlab repository, copying the extracted .iol file into the vrnetlab/cisco/iol directory, and running make docker-image

```
cp /mnt/cml/virl-base-images/ioll2-xe-17-16-01a/x86_64_crb_linux_l2-adventerprisek9-ms.iol ~/vrnetlab/cisco/iol/
cp /mnt/cml/virl-base-images/iol-xe-17-16-01a/x86_64_crb_linux-adventerprisek9-ms.iol ~/vrnetlab/cisco/iol/
```


Create docker containers from iol images

```
sudo make docker-image
```

Verify docker images 

```
sudo docker images
```

NOTE! When creating iol l2 images, the format is very picky. It needs to follow the convention in the README file exactly or it will revert to the base debian image. 

