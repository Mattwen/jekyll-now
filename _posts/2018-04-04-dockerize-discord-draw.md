---
layout: post
title: Dockerize our Node.js App and Deploy it!
---

Want to deploy your app more quickly? No need to install dependencies of Node when Docker image can handle it all for you!

# Install Docker

    wget -qO- https://get.docker.com | sh
    
Add your username to Docker group
    
    sudo usermod -aG docker matt
    
Make sure to logout and log back in

    exit
    su matt
    
Verify version of Docker

    docker --version
    Docker version 18.03.0-ce, build 0520e24
    
# Install NPM & Node.js

    sudo apt-get update
    sudo apt-get install nodejs -y
    sudo apt-get install npm -y

Verify the correct version of Node.js 

    nodejs -v
    v4.2.6

# Clone your Project from Github and install npm Dependencies
    
    cd ~
    git clone https://github.com/mattwen/discord-draw && cd discord-draw
    npm install
    
# Create the Dockerfile

With any Text Editor and add the following:

    # /home/matt/discord-draw/Dockerfile
    # Gets the latest image of node
    FROM node:carbon
    
    # Create app directory
    WORKDIR /usr/src/app

    # Install app dependencies
    # A wildcard is used to ensure both package.json AND package-lock.json are copied
    COPY package*.json ./

    RUN npm install
    # If you are building your code for production
    # RUN npm install --only=production

    # Bundle app source
    COPY . .
    # Run on port 8080
    EXPOSE 8080
    CMD [ "npm", "start" ]
    
# Create .dockerignore

Create a .dockerignore with the following and save
   
    node_modules
    npm-debug.log

# Build the Docker image

    docker build -t mattwen/discord-draw:latest .
    Successfully built 76a4c762151b
    Successfully tagged mattwen/discord-draw:latest
    
# Run our Image
    
    docker run --restart=always -p 8080:8080 -d mattwen/discord-draw:latest
    
# Verify it's Working

    curl 0.0.0.0:8080
    
Should return an HTML response

# Push to Public Docker Hub

    login docker
    Username: mattwen
    Password: 
    Login Succeeded
    
Push to the public Docker repo, where :latest is the tag name

    docker push mattwen/discord-draw:latest
    
# Docker 2 Step Deploy
If you already have Docker installed on a VM, you can install this image in two steps

    docker pull mattwen/discord-draw:latest
    docker run --restart=always -p 8080:8080 -d mattwen/discord-draw:latest
    
visit \<host_ip_address\>:8080
