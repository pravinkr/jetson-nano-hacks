# jetson-nano-hacks
Jetson nanon setup and other utilities

## Steps for jetson nano setup to make it ready for robotics vision. 
Jetson Nano I got is from [seedstudio with J101 carrier board](https://www.seeedstudio.com/NVIDIAr-Jetson-Nanotm-Developer-Kit-p-2916.html). It comes with 16 GB emmc storage and pre-installed ubuntu OS.

1. Use atleast 64 GB sdcard.
2. Flash sdcard with jetson pack. FOllow this [link](https://wiki.seeedstudio.com/Flash_System_on_SD_card/) and boot from sdcard instead of emmc.
3. Ensure ``` sudo apt update ``` doesn't raise any error. In case it does, replace sources.list at /etc/apt/ directory with this ([!sources.list](https://github.com/pravinkr/jetson-nano-hacks/blob/main/sources.list)). Notice the security.ubuntu entries are commented and only ports.ubuntu are put.
4. install cuda thru [Jetpack SDK](https://docs.nvidia.com/jetson/jetpack/install-jetpack/index.html#package-management-tool)
```
sudo apt update
sudo apt install nvidia-jetpack

```
4. install opencv - Follow this [link](https://automaticaddison.com/how-to-install-opencv-4-5-on-nvidia-jetson-nano/).
5. install ros - Follow this [link](https://www.waveshare.com/wiki/Install_ROS_System_on_Jetson_Nano_%26_Environment_Cofiguration)
```
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
sudo apt-get update
sudo apt install ros-melodic-desktop-full

# Follow instructions in the link for ros environment setup.
```
7. remote login/ssh into jetson nano machine
```
#do ip address on jetson nano and note down the ip address. should start with 192... like 192.168.29.171

ip address

# Then from another machine on the same network, connect to jetson nano using ssh or putty
ssh nvidia@192.168.29.171
```

# CSI Camera Setup and test

1. Connect mono/stereo camera via CSI port.
2. Camera Testing


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




```
