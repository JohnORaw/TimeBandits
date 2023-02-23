# Testing 1PPS inwards

Wire the PPS output of the GNSS to pin 9 of J2
![Scope Image](1PPS.jpg)

Use **testptp** to configure the SYNC_OUT pin to be an input pin.

```
sudo ./testptp  -d /dev/ptp0 -L 0,1
```

Now read some external events.
```
sudo ./testptp -e 10
```
