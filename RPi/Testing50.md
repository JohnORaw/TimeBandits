# Testing pi-ptp50
This demo uses the GNSS OEM ELT0113, wire as shown.
- Red = +5VDC
- Black = GND
- Yellow = input to UART with signal level +3V3
- 1PPS output of the GNSS board to pin #9 SYNC_OUT of header 2 (purple wire)


![pi-ptp50](pi-ptp50.jpg)

# Testing 1PPS
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
# Testing Timestamp
Ensure the UART is enabled for serial. On my system, it shows as /dev/ttyAMA0

To echo the input from the GNSS to the UART at 38,400 type the command
```
(stty 38400 -echo -icrnl; cat) </dev/ttyAMA0
```
The output will be in NMEA0183 ASCII format, something like
```
$GNRMC,110824.00,A,5510.00032,N,00726.09001,W,0.006,,300523,,,A,V*02
$GNVTG,,T,,M,0.006,N,0.012,K,A*38
$GNGGA,110824.00,5510.00032,N,00726.09001,W,1,12,0.58,115.4,M,53.9,M,,*55
$GNGSA,A,3,18,26,27,23,16,10,08,,,,,,1.05,0.58,0.88,1*0F
$GNGSA,A,3,83,73,74,66,67,82,80,,,,,,1.05,0.58,0.88,2*04
```
# Precision
This setup is fine for rough work and prototyping. When installing for fixed use, there are many more hoops to jump through.
- Compensation for antenna cable length
- Survey-In test, see the manufacturer's manual
