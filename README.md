[![npm version](https://badge.fury.io/js/janus-room.png)](https://badge.fury.io/js/janus-room)

### Janus Room

A Janus client library that provides simple interface to create a minimal-complete conference video room. This is adopted from Janus demo example code but it's JQuery-less and React/Vue friendly.

### Install

```
$ npm install
```

### Basic usage

```
import Room from 'janus-room';

...

var options = {
  server: server, // required

  // Event handlers
  onLocalJoin: onLocalJoin,
  onRemoteJoin: onRemoteJoin,
  onRemoteUnjoin: onRemoteUnjoin,
  onMessage: onMessage,
  onError: onError,
}

var room = new Room(options);
room.init()
.then(function(){
  room.register({
    room: roomId,
    username: username
  });
})
.catch(function(err){
  alert(err);
});
```

### Methods

- `room.init()` - Initialize the session.

- `room.register({room: roomId, username: username})` - Join to the room as username.
- `room.sendMessage(data)` - Send message throught Janus's DataChannel (activated by default).
- `room.attachStream(element, streamIndex)` - Attach a remote stream to a `<video>` element. Local stream is on 0.
- `room.shareScreen()` - Share screen.
- `room.stopShareScreen()` - Stop share screen and switch back to webcam.
- `room.createRoom({room:1337})` - Create new room.
- `room.removeRoom()` - Remove current room.
- `room.isShareScreenStream(streamIndex)` - Detect whether the stream is a sharescreen. Local stream is on 0.
- `room.getStream(streamIndex)` - Get stream instance by stream index.
- `room.getStreamBitrate(streamIndex)` - Get stream last bitrate by stream index.
- `room.toggleMuteAudio()` - Toggle local mic.
- `room.toggleMuteVideo()` - Toggle local video stream.
- `room.toggleVideo()` - Toggle local video stream.

Please note that toggleMute\* only mute the stream, not stop it. Use `togggleVideo()` instead to stop the video stream.

### Events (passed as params)

- `onLocalJoin(() => { ...`
- `onRemoteJoin((streamIndex, username, feedId) => { ...`
- `onRemoteUnjoin((streamIndex) => { ...`
- `onMessage((data) => { ...`
- `onVolumeMeterUpdate((streamIndex, volumeLevel) => { ...`
- `onError((err) => { ...`
- `onWarning((msg) => { ...`

### Working example

Adjust the Janus gateway URL in `example.js`, then,

- `npm install`
- `npm run-script build`
- Open `example.html` on your web browser.

### Warning

`janus-room` is still in heavy development and will makes many breaking API changes.

-----

![tarsier](https://user-images.githubusercontent.com/2534060/47661055-e06e4580-dbca-11e8-96f4-30dcdcb14c81.png)

