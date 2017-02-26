### This Repository is used to create docker base images on your ubuntu system.

Prerequisites:

Docker to be insatlled on your machine. Kindly follow the official tutorial.

Git should be installed. if not follow the below command:

```
apt-get install -y git
```

Debootstrap is required for creating Ubuntu image and rinse is needed for creating Centos Image

```
apt-get install debootstrap
```

Sample Output:

```
apt-get install debootstrap
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following NEW packages will be installed:
  debootstrap
0 upgraded, 1 newly installed, 0 to remove and 86 not upgraded.
Need to get 37.6 kB of archives.
```

```
apt-get install rinse
```

Sample Output:

```
apt-get install rinse
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following NEW packages will be installed:
  rinse
0 upgraded, 1 newly installed, 0 to remove and 86 not upgraded.
```

Now clone the repository of docker from Github.

```
git clone https://github.com/docker/docker.git
```

Sample Output

```
git clone https://github.com/docker/docker.git
Cloning into 'docker'...
remote: Counting objects: 215300, done.
remote: Compressing objects: 100% (25/25), done.
remote: Total 215300 (delta 4), reused 0 (delta 0), pack-reused 215275
Receiving objects: 100% (215300/215300), 121.60 MiB | 5.30 MiB/s, done.
Resolving deltas: 100% (141701/141701), done.
Checking connectivity... done.
```

Now we can run the script to create a base image of ubuntu or centos. Script are present in docker/contrib/ folder.

```
cd docker/contrib/
```

####Creating Ubuntu Image on Ubuntu Machine, follow the below command

```
./mkimage.sh -t schoolofdevops/ubuntu debootstrap --include=ubuntu-minimal --components=main,universe trusty
```

```
./mkimage.sh -t schoolofdevops/ubuntu debootstrap --include=ubuntu-minimal --components=main,universe trusty
+ mkdir -p /var/tmp/docker-mkimage.n6jNGOcdJm/rootfs
+ debootstrap --include=ubuntu-minimal --components=main,universe trusty /var/tmp/docker-mkimage.n6jNGOcdJm/rootfs
I: Retrieving InRelease
I: Failed to retrieve InRelease
I: Retrieving Release
I: Retrieving Release.gpg
I: Checking Release signature
I: Valid Release signature (key id 790BC7277767219C42C86F933B4FE6ACC0B21F32)
```

After this is created we can test the created image by,

```
docker images
```

Sample Output

```
root@iso:/docker/contrib# docker images
REPOSITORY              TAG                 IMAGE ID            CREATED             SIZE
schoolofdevops/ubuntu   latest              238e5a24f614        25 minutes ago      175 MB
```

We can also try accessing the image,

```
docker run -it schoolofdevops/ubuntu /bin/bash
```

Sample Output

```
docker run -it schoolofdevops/ubuntu /bin/bash
root@9ff2a2f29512:/#
root@9ff2a2f29512:/#uname -v
#85-Ubuntu SMP Mon Feb 20 11:50:30 UTC 2017
```

####Creating Centos Image on Ubuntu Machine, follow the below command

```
./mkimage.sh -t schoolofdevops/centos:6 rinse --distribution centos-6
```

Sample Output
```
./mkimage.sh -t schoolofdevops/centos:6 rinse --distribution centos-6
+ mkdir -p /var/tmp/docker-mkimage.f3VBlBLpU9/rootfs
+ rinse --directory /var/tmp/docker-mkimage.f3VBlBLpU9/rootfs --arch amd64 --distribution centos-6
[4:111] Downloading    : binutils-2.20.51.0.2-5.44.el6.x86_64.rpm ..
```

After this is created we can test the created image by,

```
docker images
```

Sample Output

```
docker images
REPOSITORY                   TAG                   IMAGE ID            CREATED             SIZE
schoolofdevops/centos         6                   aaa6f86c7ae7        45 minutes ago      207 MB
```

We can also try accessing the image,

```
docker run -it schoolofdevops/centos:6 /bin/bash
```

Sample Output

```
docker run -it schoolofdevops/centos:6 /bin/bash
bash-3.2#
bash-3.2#
bash-3.2# which yum
/usr/bin/yum
```
