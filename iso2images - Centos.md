### This Repository is used to create docker base images on your Centos system.

Prerequisites:

Docker to be insatlled on your machine. Kindly follow the official tutorial.
Git should be installed. if not follow the below command:

```
yum install -y git
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
./mkimage-yum.sh schoolofdevops/centos
```

```
[root@centos contrib]# ./mkimage-yum.sh schoolofdevops/centos
+ mkdir -m 755 /tmp/mkimage-yum.sh.hVotrr/dev
+ mknod -m 600 /tmp/mkimage-yum.sh.hVotrr/dev/console c 5 1
+ mknod -m 600 /tmp/mkimage-yum.sh.hVotrr/dev/initctl p
+ mknod -m 666 /tmp/mkimage-yum.sh.hVotrr/dev/full c 1 7
+ mknod -m 666 /tmp/mkimage-yum.sh.hVotrr/dev/null c 1 3
+ mknod -m 666 /tmp/mkimage-yum.sh.hVotrr/dev/ptmx c 5 2
+ mknod -m 666 /tmp/mkimage-yum.sh.hVotrr/dev/random c 1 8
+ mknod -m 666 /tmp/mkimage-yum.sh.hVotrr/dev/tty c 5 0
+ mknod -m 666 /tmp/mkimage-yum.sh.hVotrr/dev/tty0 c 4 0
+ mknod -m 666 /tmp/mkimage-yum.sh.hVotrr/dev/urandom c 1 9
+ mknod -m 666 /tmp/mkimage-yum.sh.hVotrr/dev/zero c 1 5
```

After this is created we can test the created image by,

```
docker images
```

Sample Output

```
docker images
REPOSITORY              TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
schoolofdevops/centos   6.8                 f795886b4f50        19 seconds ago      183.2 MB
```

We can also try accessing the image,

```
docker run -it schoolofdevops/ubuntu /bin/bash
```

Sample Output

```
[root@centos contrib]# docker run -it schoolofdevops/centos:6.8 /bin/bash
[root@a24a0236a418 /]#
[root@a24a0236a418 /]#
[root@a24a0236a418 /]# which yum
/usr/bin/yum
[root@a24a0236a418 /]#
```
