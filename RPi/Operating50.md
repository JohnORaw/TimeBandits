# Operating pi-ptp50
Create a ptp.config file to define any common parameters. If the GNSS is connected via USB, the device name may be /dev/ttyACM0
```
[global]
ts2phc.nmea_serialport /dev/ttyAMA0
leapfile leap-seconds.list
tx_timestamp_timeout 100
[eth0]
```


