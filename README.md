# jetson-nano-hacks
Jetson nanon setup and other utilities

## Steps for jetson nano setup to make it ready for robitics vision. 
Jetson Nano I got is from seedstudio with J101 carrier board. It comes with 16 GB emmc storage and pre-installed ubuntu OS.

1. Use atleast 64 GB sdcard.
2. install cuda thru [Jetpack SDK](https://docs.nvidia.com/jetson/jetpack/install-jetpack/index.html#package-management-tool)
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
7. 
