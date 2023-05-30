# Testing pi-ptp50
This demo uses the GNSS OEM ELT0113, wire as shown.
- Red = +5VDC
- Black = GND
- Yellow = input to UART with signal level +3V3
- 1PPS output of the GNSS board to pin #9 of header 2 (purple wire)
![pi-ptp50](pi-ptp50.jpg)

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
