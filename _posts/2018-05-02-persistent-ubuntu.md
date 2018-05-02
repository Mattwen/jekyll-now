---
layout: post
title: Create Persistant Ubuntu Shell and Install Ruby
---

(If you already have Docker you can skip to the end)

# Install Docker
```sh
wget -qO- https://get.docker.com | sh
```
Add your username to Docker group
```sh
sudo usermod -aG docker matt
```
Make sure to logout and log back in
```sh
exit
su matt
```
Verify version of Docker
```sh
docker --version
Docker version 18.03.0-ce, build 0520e24
```

Start an Ubuntu 16.04 shell
```
docker run -it ubuntu:latest /bin/bash
apt-get update
apt-get install ruby-full -y
```

WIP
