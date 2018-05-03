---
layout: post
title: Create Persistant Ubuntu Shell and Install Ruby
---

You can create many Ubuntu 16.04 isolated environments this way, no need to worry about conflicting apps and dependencies. 

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
# Create the Bash Shell
Start an Ubuntu 16.04 shell
```sh
docker run --name rubyshell --restart=always -it ubuntu:latest /bin/bash
exit
```

Create an Alias with name 'rubyshell' to access the shell more quickly
```sh
alias rubyshell="docker exec -it rubyshell /bin/bash"
rubyshell
root@40545a72cb07:/# 
```

Install your desired depenencies
```sh
apt-get install build-essential -y
apt-get install ruby-full -y
apt-get install git -y
```

Verify the version of Ruby
```sh
ruby -v
ruby 2.5.1p57 (2018-03-29 revision 63029) [x86_64-linux-gnu]
```

If you want to use this template again, commit the change to a new image (this can take a little while)
```sh
docker commit rubyshell rubyshell:latest
sha256:3f292619593e10b1dc137f8a3526e4b23f9e4d7d9115f136e80d3e74c6a8562f
```

To start a new container from that newly created image: 
```sh
docker run --name rubyshell2 --restart=always -it rubyshell:latest /bin/bash
root@11f2cfa4aab6:/# 
```
It will have everything configured from your last image. If you want them to share data create a persistant shared volume
Creates alias for all your containers or create a .bashrc function that accepts a name parameter for your container
