---
layout: post
title: Scale our Docker App on Multiple Ports
---
Want to be able to scale you application so it has mutiple instances of the same app? We can do this by running the app on a particular port.

# Create 3 Docker containers from our Image
This will assign each instance a random and unused port from Docker named instance1, instance2, instance3
```sh
docker run -d -P --name instance1 mattwen/discord-draw:latest
docker run -d -P --name instance2 mattwen/discord-draw:latest
docker run -d -P --name instance3 mattwen/discord-draw:latest
```
Review the port numbers
```sh
docker container list -a
```
Docker created the app on ports 32768-32770 and directs to internal port 8080 (the port that the app is running on)

![Imgur](https://i.imgur.com/WM9gjFC.png)

Inside Google Cloud Dashboard > Hamburger(Top Left corner) > VPC Network > Firewall Rules
Create a Google Cloud VPN Exception for the new ports:

![Imgur](https://i.imgur.com/YP9JoEM.png)

Add a name and the following information:

![Imgur](https://i.imgur.com/uzMQ4Rg.png)

Visit the public ip address of your Compute Engine VM and verify it's working!

![Imgur](https://i.imgur.com/0rIA9fI.png)

Each port resolution now has it's own unique app running inside of it!
