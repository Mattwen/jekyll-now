---
layout: post
title: Node.js Draw with friends!
---
Interactive Demo: [http://draw.mwenger.io](http://draw.mwenger.io)
-
-
-
![Example](https://i.imgur.com/jZp7WuZ.png)

-Uses Websockets to render lines concurrently across devices/ browsers!
-Stores up to 2500 lines on the server. Sorry if you want it to store more than need to use a beefier Cloud instance. Or maybe I should cache the lines in the browser?

Node.js application deployed with pm2 and Google Cloud instance.
-PM2 is really easy to install and can even deploy Python and Ruby apps! Basically any app that can be ran at a bash command line can be ran with PM2
![PM2 App](https://i.imgur.com/oYCNC7c.png)
App deployed on PM2 and Google Cloud VM instance

# discord-draw
Basic drawing application for your users.
example: http://yourdomain.com

# Install for yourself on Ubuntu 16.04!

git clone

    git clone https://github.com/Mattwen/discord-draw.git
    cd discord-draw
    sudo chmod +x server.js
    
install required npm packages

    npm install
    
check to see if it's running properly

    sudo node server.js
    
deploy on pm2 (you need node env + pm2 installed first)

    sudo pm2 start
    pm2 start server.js -n "whatever-you-like"



