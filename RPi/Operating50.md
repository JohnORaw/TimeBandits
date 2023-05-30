# Operating pi-ptp50
Firstly, I create a ptp.config file to define any common parameters.

```
[global]
ts2phc.nmea_serialport /dev/ttyAMA0
leapfile leap-seconds.list
tx_timestamp_timeout 100
[eth0]
```


