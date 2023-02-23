# Setup PPS out from CM4

On J2, pin 8 = SYNC_IN, pin 9 = SYNC_OUT

A number of commentators say pin 8 is not wired, to be verified.

Run the following commands to get a 1 PPS output, it is c. 6µs wide and 3V3. 
```
sudo ./testptp -d /dev/ptp0 -L0,2
sudo ./testptp -d /dev/ptp0 -p 1000000000
```

![Scope Image](1PPS.jpg)
