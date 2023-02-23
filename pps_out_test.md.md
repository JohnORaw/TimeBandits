Using a generic CM4 IO Board, install linuxptp

IO board manual https://datasheets.raspberrypi.com/cm4io/cm4io-datasheet.pdf

```
sudo apt install linuxptp
```
Get testptp from repo https://github.com/torvalds/linux/blob/master/tools/testing/selftests/ptp/testptp.c and compile
```
gcc testptp.c -o testptp
./testptp -h
```
Run the following commands to get a 1 PPS output. 
On J2, pin 8 = SYNC_IN, pin 9 = SYNC_OUT
A number of commentators say pin 8 is not wired, to be verified.
```
sudo ./testptp -d /dev/ptp0 -L0,2
sudo ./testptp -d /dev/ptp0 -p 1000000000
```
![Scope Image](1PPS.jpg)
