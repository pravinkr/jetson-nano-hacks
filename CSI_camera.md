# CSI Camera Setup and test

## Testing using opencv

Clone this [repo](https://github.com/pravinkr/jetson-nano-hacks-CSI-Camera) and run python scripts to test single and dual cameras.
```
$ python simple_camera.py
$ python face_detect.py
$ python3 dual_camera.py

```




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
# Simple Test
#  Ctrl^C to exit
# sensor_id selects the camera: 0 or 1 on Jetson Nano B01
$ gst-launch-1.0 nvarguscamerasrc sensor_id=0 ! nvoverlaysink

$ gst-launch-1.0 nvarguscamerasrc ! 'video/x-raw(memory:NVMM), width=(int)1920, height=(int)1080,format=(string)NV12, framerate=(fraction)30/1' ! nvoverlaysink

$ gst-launch-1.0 nvarguscamerasrc ! nvoverlaysink

$ gst-launch-1.0 nvarguscamerasrc sensor_id=0 ! \
   'video/x-raw(memory:NVMM),width=1920, height=1080, framerate=30/1' ! \
   nvvidconv flip-method=0 ! 'video/x-raw,width=960, height=540' ! \
   nvvidconv ! nvegltransform ! nveglglessink -e
   
```

## Stereo camera driver for ROS.
The driver is needed to capture images from left and right camera and publish on ros image topics.

Follow this [link](https://github.com/borongyuan/jetson_csi_stereo_ros) for ros driver/packages installation.


