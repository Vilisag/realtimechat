## The demo Realtime chat by NodeJs

### 1. Intall

~~~bash
npm install
~~~

### 2. Run

~~~bash
node app.js

or

nodemon app.js
~~~

### 3. Code

~~~javascript
var app = require('express')();
var http = require('http').Server(app);
var io = require('socket.io')(http);

const port = 3000;

app.get('/', function(req, res) {
    res.sendFile(__dirname + '/index.html');
});

io.on('connection', function(socket) {
    console.log('user connected');
    socket.broadcast.emit('hi');
    socket.on('chat message', function(msg) {
        io.emit('chat message', msg);
    });
    socket.on('disconnect', function() {
        console.log('user disconnected');
    });
});

http.listen(port, function() {
    console.log(`The server is listening on http://localhost:${port}`);
});
~~~
