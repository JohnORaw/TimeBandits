# Using generic CM4 IO Boards
Connect to a live network, do updates to begin
```
sudo apt update
sudo apt upgrade -y
```
The IO board manual can be found at https://datasheets.raspberrypi.com/cm4io/cm4io-datasheet.pdf

## Hardware Checks
Check that the Ethernet card supports hardware time stamping
```
ethtool -T eth0
```
## Set the hostname

Edit /etc/hostname and /etc/hosts to the correct hostnames

- PtP Master is pi-ptp50
- PtP Slave is pi-ptp51

## Set static IP addresses
Edit /etc/dhcpcd.conf 

pi-ptp50 is
```
# Static IP configuration:
interface eth0
static ip_address=192.168.3.50/24
static routers=192.168.3.10
static domain_name_servers= 8.8.8.8
```
pi-ptp51 is
```
# Static IP configuration:
interface eth0
static ip_address=192.168.3.51/24
static routers=192.168.3.10
static domain_name_servers=8.8.8.8
```
## Get testptp
Download the source and compile
```
 wget https://raw.githubusercontent.com/torvalds/linux/master/tools/testing/selftests/ptp/testptp.c
 gcc -o testptp testptp.c -lrt
```
