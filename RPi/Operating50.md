# Operating pi-ptp50
Create a ptp.config file to define any common parameters. If the GNSS is connected via USB, the device name may be /dev/ttyACM0
```
[global]
ts2phc.nmea_serialport /dev/ttyAMA0
leapfile leap-seconds.list
tx_timestamp_timeout 100
[eth0]
```
Synchronize the PTP hardware clock from the GNSS, verify.
```
sudo ts2phc -f ptp.config -s nmea -m -q -l 7
```
The master offset settles down over time.

```
ts2phc[72.332]: eth0 extts index 0 at 1685452383.999999997 corr 0 src 1685452384.935373093 diff -3
ts2phc[72.332]: eth0 master offset         -3 s2 freq   -2261
ts2phc[73.340]: nmea delay: 142607833 ns
ts2phc[73.340]: eth0 extts index 0 at 1685452385.000000001 corr 0 src 1685452385.943398734 diff 1
ts2phc[73.340]: eth0 master offset          1 s2 freq   -2258
ts2phc[73.400]: nmea sentence: GNRMC,131228.00,A,5510.00075,N,00726.09158,W,0.008,,300523,,,A,V
ts2phc[74.348]: nmea delay: 145597639 ns
```

