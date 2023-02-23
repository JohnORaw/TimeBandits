Using a generic CM4 IO Board, install linuxptp

```
sudo apt install linuxptp
```
Get testptp from repo https://github.com/torvalds/linux/blob/master/tools/testing/selftests/ptp/testptp.c and compile
```
gcc testptp.c -o testptp
./testptp -h
```
Run the following commands to get a 1 PPS output.
```
sudo ./testptp -d /dev/ptp0 -L0,2
sudo ./testptp -d /dev/ptp0 -p 1000000000
```
![](1pps.jpg)
