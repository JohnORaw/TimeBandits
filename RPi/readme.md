# Configuring a pair of RPi CM4 as a PtP testbed
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
