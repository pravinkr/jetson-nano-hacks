# CSI Camera Setup and test

## Test using nvgstcapture
### Follow tutorial on [nvidia site](https://developer.nvidia.com/embedded/learn/tutorials/first-picture-csi-usb-camera)

```
nvgstcapture-1.0 --help

# Test for csi camera on /dev/video0
nvgstcapture-1.0
nvgstcapture-1.0 --orientation 2

# Testing multiple csi input cameras

nvgstcapture-1.0 --orientation 2 --sensor-id=0
nvgstcapture-1.0 --orientation 2 --sensor-id=1

```


## Test using gst-launch-1.0/Gstreamer
[Installing gstreamer](https://gstreamer.freedesktop.org/documentation/installing/on-linux.html?gi-language=c)

```
apt-get install libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev libgstreamer-plugins-bad1.0-dev gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-libav gstreamer1.0-doc gstreamer1.0-tools gstreamer1.0-x gstreamer1.0-alsa gstreamer1.0-gl gstreamer1.0-gtk3 gstreamer1.0-qt5 gstreamer1.0-pulseaudio
```

```
gst-launch-1.0 nvarguscamerasrc ! 'video/x-raw(memory:NVMM), width=(int)1920, height=(int)1080,format=(string)NV12, framerate=(fraction)30/1' ! nvoverlaysink

gst-launch-1.0 nvarguscamerasrc ! nvoverlaysink
```
