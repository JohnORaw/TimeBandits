# Software Install
## Install PtP
The generic version in the repo has some downsides, but it works for these tests.
```
sudo apt install linuxptp
```
## Get TestPtP
Get testptp from repo https://github.com/torvalds/linux/blob/master/tools/testing/selftests/ptp/testptp.c and compile
```
gcc -o testptp testptp.c -lrt
./testptp -h
```
Check that ptp devices show
```
ls /dev
```

Check that the Ethernet card supports hardware time stamping. Make sure to use the correct card label, mine was eth0.

```
ethtool -T eth0
```