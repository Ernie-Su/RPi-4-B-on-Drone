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

### References:
https://github.com/mavlink/qgroundcontrol/tree/master/src/VideoReceiver#linux
