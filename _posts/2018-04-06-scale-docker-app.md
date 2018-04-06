---
layout: post
title: Scale our Docker App on Multiple Ports
---

# Create 3 Docker containers from our Image
This will assign each instance a random and unused port from Docker named instance\<1-3\>
```sh
docker run -d -P --name instance1 mattwen/discord-draw:latest
docker run -d -P --name instance2 mattwen/discord-draw:latest
docker run -d -P --name instance3 mattwen/discord-draw:latest
```
Review the port numbers
```sh
docker container list -a
```
Docker created the app on ports 32768-32770
![Imgur](https://i.imgur.com/WM9gjFC.png)

Create a Google Cloud VPN Exception for the new ports:
![Imgur](https://i.imgur.com/YP9JoEM.png)

Add a name and the following information:

![Imgur](https://i.imgur.com/uzMQ4Rg.png)

Visit the public ip address of your Compute Engine VM and verify it's working!

![Imgur](https://i.imgur.com/5pAgOiE.png)

Each port resolution now has it's own unique app running inside of it!
