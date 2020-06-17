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
receiver:
or QGC

***

### References:
