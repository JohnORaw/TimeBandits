# Configuring a RPi CM4 as a PtP Grand Master
This requires a GNSS, preferably with a UBX ZED R9T chip. For this project, the case mounting [ELT0113](https://gnss.store/zed-f9t-timing-gnss-modules/129-elt0113.html) was used. 

Using sudo **raspi-config** enable the first UART as a serial port.  

To enable the additional ports, edit /boot/config.txt at the end
```
# Changes by JOR
dtoverlay = uart2
dtoverlay = uart3
dtoverlay = uart4
dtoverlay = uart5
```
Identify the location of each UART using 

```
dtoverlay -h uart2
dtoverlay -h uart3
dtoverlay -h uart4
dtoverlay -h uart5
```
This give the GPIO location. Locate which pin on the header using 
```
dtoverlay -h uart2
```

