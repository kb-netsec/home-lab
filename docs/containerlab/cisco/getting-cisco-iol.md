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

Copy iol binaries to vrnetlab/cisco/iol 7/9/2026 UPDATE: TL;DR, this is now a big pain in the neck. According to AI slop, Staring with (CML) 2.10, the Cisco IOS on Linux (IOL) images are no longer provided as standalone .iol files in the reference platform (refplat) ISO. Instead, they are packaged as docker devices within a compressed archive (e.g., iol-xe-17-18-02.tar.gz) containing blob files with SHA256 hash names

To extract the usable IOL binary for use in emulators like GNS3 or Containerlab, you must perform the following steps:

Extract the tar.gz archive from the ISO to a temporary directory. You can't extract them to the mount point as it's read only. (Ask me how I know.)

```
# 1. Create a working directory in your home folder
mkdir -p ~/cml_extract
cd ~/cml_extract

# 2. Copy the archive from the ISO to your local directory
cp /mnt/CML/virl-base-images/iol-xe-17-18-02/iol-xe-17-18-02.tar.gz .

# 3. Extract the outer tar.gz archive (this creates the 'blobs' folder)
# Use -z for gzip, -x for extract, -v for verbose, -f for file
tar -xzvf iol-xe-17-18-02.tar.gz
```

Navigate to the blobs directory (blobs/sha256/) and identify the largest file (typically ~287MB). 

```
# List files and sort by size to find the largest blob (usually the OS image)
ls -lhS

# Verify the file type (it should say "POSIX tar archive")
file <largest_file_hash>
# Example output: ac697212...: POSIX tar archive   
```


Extract the inner POSIX tar archive from that specific blob file.

```
# Extract the specific .iol file directly from the blob
# Replace <hash_file> with the actual filename (e.g., ac697212...)
# Replace <iol_filename> with the target binary name found in step 1
tar -xf <hash_file> <iol_filename>
```

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

