# dash-hls-stream
A simple setup for live streaming RTMP to DASH and HLS with a focus on low latency.

* Simple web UI using dash.js and native HTML5 video for HLS
* Javascript detection for iOS
* Configurable using environment variables
* Supports security using stream key authentication

This project is a downstream of [alfg/nginx-rtmp](https://github.com/alfg/docker-nginx-rtmp)

## Usage

### Docker
```
docker run -it -p 1935:1935 -p 80:8080 sjsmart/dash-hls-stream
```

### Docker Compose
```
services:
  dash:
    image: sjsmart/dash:latest
    ports:
      - '8080:8080'
      - '1935:1935'
    environment:
      DASH_STREAM_KEY: 'examplestreamkey'
      DASH_PROJECT_NAME: 'My Stream'
```

## Parameters
| Parameter | Function |
| :----: | --- |
| `-e DASH_PROJECT_NAME=ProjectName` | Used for the Web UI header and page title |
| `-e DASH_STREAM_KEY=examplekey` | Only this stream key will be accepted |
| `-e DASH_LIVE_DELAY=2` | Dash.js [setLiveDelay()](http://cdn.dashjs.org/latest/jsdoc/module-MediaPlayer.html#setLiveDelay__anchor) |
| `-e DASH_LATENCY_MIN_DRIFT=0.05` | Dash.js [setLowLatencyMinDrift()](http://cdn.dashjs.org/latest/jsdoc/module-MediaPlayer.html#setLowLatencyMinDrift__anchor) |
| `-e DASH_CATCHUP_PLAYBACK_RATE=0.2` | Dash.js [setCatchUpPlaybackRate()](http://cdn.dashjs.org/latest/jsdoc/module-MediaPlayer.html#setCatchUpPlaybackRate__anchor) |
