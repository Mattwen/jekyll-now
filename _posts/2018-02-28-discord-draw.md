---
layout: post
title: Deploy a Node.js Drawing App
---
Interactive Demo: [http://draw.mwenger.io](http://draw.mwenger.io)

Github Repository: [link](https://github.com/Mattwen/discord-draw)

![Example](https://i.imgur.com/jZp7WuZ.png)

Uses Websockets to render lines concurrently across devices/ browsers!

* Stores up to 2500 lines on the server before it starts cleaning house.
* Sorry if you want it to store more than need to use a beefier cloud instance.
* Node.js application deployed with PM2 and Google Cloud instance.

PM2 is really easy to install and can even deploy Python and Ruby apps! Basically any app that can be ran at a bash command line can be ran with PM2

![PM2 App](https://i.imgur.com/oYCNC7c.png)
App deployed on PM2 and Google Cloud VM instance

# discord-draw
Basic drawing application for your users.
example: http://yourdomain.com

# Server.js
line_history has three objerct types: Size defines the size the point, Color defines the color of the point, and Data is simply the X, Y coordinates of line.

socket.emit broadcasts the objects to all connected clients on the browser so everything is synchronized.

```ruby
# Store line history
var line_history = [];

// event-handler for new incoming connections
io.on('connection', function (socket) {
    // first send the history to the new client
    for (var i in line_history) {
        socket.emit('draw_line', {size: line_history[i].Size, color: line_history[i].Color,  line: line_history[i].Data});
    }
    // add handler for message type "draw_line".
    socket.on('draw_line', function (data) {

        // add input to line_history objects
        var input = {
            'Size': data.size, // size of the brush
            'Color': data.color, // color of the line
            'Data': data.line // position of the line
        }
        // push objects to add
        line_history.push(input);

        // remove the first 150 objects from the array list if the total array list exceeds 2500 entries
        if(line_history.length >= 2500){
            line_history.splice(0, 150);
        }
        
        // send line to all clients
        io.emit('draw_line', { size: data.size, color: data.color, line: data.line });
    });
});
```

Uses Express and socketIo to create a websocket and runs on localhost and port 8080
```ruby
var express = require('express'),
    app = express(),
    http = require('http'),
    socketIo = require('socket.io');

// start webserver on port 8080
var server = http.createServer(app);
var io = socketIo.listen(server);
server.listen(8080);
// add directory with our static files
app.use(express.static(__dirname + '/'));
console.log("Server running on 127.0.0.1:8080");
```

# Client.js

Too long to inline so client.js can be found here: [link](https://github.com/Mattwen/discord-draw/blob/master/client.js)

Basically, client.js handles all client side stuff like drawing the canvas, drawing lines defined by socket, recording mouse movements, using form controls to change brush size, color, and etc.

# Install for yourself on Ubuntu 16.04!

    git clone https://github.com/Mattwen/discord-draw.git
    cd discord-draw
    sudo chmod +x server.js

install required npm packages
```sh
    npm install
```    
check to see if it's running properly
```sh
    sudo node server.js
```    
deploy on pm2 (you need node env + pm2 installed first)
```sh
    sudo pm2 start
    pm2 start server.js -n "whatever-you-like"
```


