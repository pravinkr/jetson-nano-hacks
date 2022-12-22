# CSI Camera Setup and test

```
gst-launch-1.0 nvarguscamerasrc ! 'video/x-raw(memory:NVMM), width=(int)1920, height=(int)1080,format=(string)NV12, framerate=(fraction)30/1' ! nvoverlaysink

gst-launch-1.0 nvarguscamerasrc ! nvoverlaysink
```
