# RPi 4 B on Drone
## Overclock

```sudo vi /boot/config.txt```

CPU:

Add the following in config.txt:

```
over_voltage=4
arm_freq=2000
```

To insepct the CPU frequency, ```watch -n 1 vcgencmd measure_clock arm```

GPU:

Add the following in config.txt:

```gpu_freq=600```

After every change, you have to reboot to find out whether the change works on RPi.

```sudo reboot```

***

## gstreamer
sender:

```
gst-launch-1.0 videotestsrc ! video/x-raw,width=640,height=480 ! videoconvert ! x264enc ! rtph264pay ! udpsink host=127.0.0.1 port=5600
```

receiver:

```
gst-launch-1.0 udpsrc port=5600 caps='application/x-rtp, media=(string)video, clock-rate=(int)90000, encoding-name=(string)H264' ! rtpjitterbuffer ! rtph264depay ! h264parse ! avdec_h264 ! autovideosink fps-update-interval=1000 sync=false
```

or QGC

***

# Deploy model on companion computer
1. imageset --(LabelImg)--> xml --(convert)--> csv --(convert)--> tfrecord --(as input)--> Tensorflow Object Detection API train

  Got a lot of errors here, gave up. (Haven't try resize from 512 to 300 yet!)
  
2. imageset --(LabelImg)--> xml --(convert)--> VOC2007 --> train ssd --> get model's .pb --> get .pb and .pbtxt --(as model input)--> opencv.dnn

  Also got a lot of errors here, but changed img size from 512 to 300 and train.py works. However, got suck results while training.


### References:
https://github.com/mavlink/qgroundcontrol/tree/master/src/VideoReceiver#linux
