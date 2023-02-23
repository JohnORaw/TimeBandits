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