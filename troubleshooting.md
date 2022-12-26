# Issues encounered and solution

1. gstreamer crashing with below error

Error generated. /dvs/git/dirty/git-master_linux/multimedia/nvgstreamer/gst-nvarguscamera/gstnvarguscamerasrc.cpp, execute:751 Failed to create CaptureSession
Solution: Refer this [link](https://forums.developer.nvidia.com/t/error-generated-gstnvarguscamerasrc-cpp-execute-543-failed-to-create-capturesession/112431) for solution.
  This may happen if there is another session using this same camera (hung or alive) and try to use same camera again; if this issue is happening sometimes. You can close all sessions and reset the nvargus-daemon to reset the argus framework and try nvgstcapture-1.0 again.

  sudo service nvargus-daemon restart
