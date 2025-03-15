# WebRTC - youtube - Robbert Bunch - webrtc starter

## Setup https (certs):
1. npm install mkcert -g
2. mkcert create-ca
3. mkcert create-cert
4. OPTIONAL: to run it locally, update the files with your local IP
    - if using a phone or another computer (ipconfig to get local ip)

## setup server.js
- create our socket.io server
- add local ip address to cors origins

```js
//server.js
const io = socketio(expressServer,{
    cors: {
        origin: [
            'https://localhost:8181',
            'https://192.168.1.103:8181' //if using a phone or another computer (ipconfig to get local ip)
        ],
        methods: ["GET", "POST"]
    }
});
```

## setup scripts.js
- connect to socket server

```js
// scripts.js
//if trying it on a phone, use this instead...
const socket = io.connect('https://192.168.1.103:8181',{
// const socket = io.connect('https://localhost:8181',{
    auth: {
        userName,password
    }
})
```

## talking through the code
- starts at 43:09 index.html
    - `<video id="local-video"></video>`
    - `<video id="remote-video"></video>`

- note with: `<script src="/socket.io/socket.io.js"></script>` this is how to include `socket.io.js` when putting it in html
- gives access to `io` in the code eg. `io.connect()`

- `scripts.js` - webrtc related
    - send userName and password on connecting to socket server

- `socketListeners.js` - socket related

- `server.js` 
    - `const express = require('express');`
    - `const socketio = require('socket.io');`
    - fs module toget contents of cert.key and cert.crt (used for creating the server)
    - cors origin lists valid domains you can visit the server from (NOTE: port NOT included here)
        - https://localhost
        - https://192.168.1.44
    - get access to passed in username + password 

    ```js
    const userName = socket.handshank.auth.userName;
    const password = socket.handshank.auth.password;

    //validate the password
    if(password !== ""){
        socket.disconnect(true);
    }
    ```