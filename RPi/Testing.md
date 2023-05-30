# Testing
Connect the 1PPS output of the GNSS board to pin #9 of header 2
Set pin zero to external time stamp and test

```
sudo ./testptp  -d /dev/ptp0 -L 0,1
sudo ./testptp  -d /dev/ptp0 -e 5
```
