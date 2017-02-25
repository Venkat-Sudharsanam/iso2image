This repo is to convert your **Ubuntu** machine into a docker image. Make sure that the docker has been installed on your machine and continue the below steps

### Removing the unwanted packages
```
apt remove iwl* ql* xorg* ipw* ghostscript* libtheora systemtap-runtime alsa* mysql-libs iw hicolor-icon-theme *firmware* -y
apt-get clean all
```
Now creating a Tar out of the current working machine:

```
tar --numeric-owner --exclude=/proc --exclude=/sys --exclude=/mnt --exclude=/usr/share/{foomatic,backgrounds,perl5,fonts,cups,qt4,groff,kde4,icons,pixmaps,emacs,gnome-background-properties,sounds,gnome,games,desktop-directories} --exclude /var/lib/docker -zcvf /mnt/Ubuntu-xenial-base.tar.gz /
```

Now we need to import the tar which we created:

```
cat /mnt/Ubuntu-xenial-base.tar.gz | docker import - ubuntu16.04xenial:1.0.0
```
Sample output:

```
cat /mnt/Ubuntu-xenial-base.tar.gz | docker import - ubuntu16.04xenial:1.0.0
sha256:46294fd7df9f617dc2a13942e8adf838c39e4406eb11ab7b77a5af803b025b15   
``` 
We can check it buy:

```
docker images
```

Sample Output:

```
docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu16.04xenial   1.0.0               46294fd7df9f        5 minutes ago       748 MB
```   

Now create a container out of the image and test it:

```
docker run -it ubuntu16.04xenial:1.0.0 /bin/bash
```

Sample Output:

```
root@iso:/# docker run -it ubuntu16.04xenial:1.0.1 /bin/bash
root@722eb61db0bb:/# sudo su
```
