# Testing50

## Testing pi-ptp50

This demo uses the GNSS OEM ELT0113, wire as shown.

* Red = +5VDC
* Black = GND
* Yellow = input to UART with signal level +3V3
* 1PPS output of the GNSS board to pin #9 SYNC\_OUT of header 2 (purple wire)

![pi-ptp50](../.gitbook/assets/pi-ptp50.jpg)

## ptp.config

My ptp.config file was as follows

```
[global]
ts2phc.nmea_serialport /dev/ttyAMA0
leapfile leap-seconds.list
tx_timestamp_timeout 100
[eth0]
```

## Testing 1PPS

Set pin zero to external time stamp and test

```
sudo ./testptp  -d /dev/ptp0 -L 0,1
sudo ./testptp  -d /dev/ptp0 -e 5
```

The resulting output should be something like

```
johnoraw@pi-ptp50:~ $ sudo ./testptp  -d /dev/ptp0 -e 5
external time stamp request okay
event index 0 at 2433.874481064
event index 0 at 2434.874478136
event index 0 at 2435.874475200
event index 0 at 2436.874472256
event index 0 at 2437.874469320
```

## Testing Timestamp

Ensure the UART is enabled for serial. On my system, it shows as /dev/ttyAMA0

To echo the input from the GNSS to the UART at 38,400 type the command

```
(stty 38400 -echo -icrnl; cat) </dev/ttyAMA0
```

The output will be in NMEA0183 ASCII format, something like

```
$GNRMC,110824.00,A,5510.00032,N,00726.09001,W,0.006,,300523,,,A,V*02
```

## Precision

This setup is fine for rough work and prototyping. When installing for fixed use, there are many more hoops to jump through.

* Compensation for antenna cable length
* Survey-In test, see the manufacturer's manual
