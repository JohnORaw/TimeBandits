# Meta Server 
These are the build instruction for the time server in the KMN data centre. 
This server is intended to synch a local hardware clock via GNSS.

## Initial Setup
The hardware is a legacy Dell PE R520. The server was set to UEFI Boot and UB2204 was installed from a USB key. IP address is via DHCP and only interface *eno1* has a connection. Updates were carried out.
```
sudo apt update
sudo apt upgrade -y
```

The latest version of LinuxPTP is downloaded.
```
wget https://sourceforge.net/projects/linuxptp/files/v3.1/linuxptp-3.1.1.tgz/download

```
The download file is renamed and extracted.
- x for extract
- v for verbose
- z for gnuzip
- f for filename, which must be at the end.
```
mv download linuxptp-3.1.1.tgz
tar -xvzf ./linuxptp-3.1.1.tgz
```
**make** and **gcc** are installed.
```
sudo apt install make gcc
```
Working directory is changed to ./linuxptp-3.1.1

**make** is run, this should build the current version of the application. Check for errors!
```
cd linuxptp-3.1.1/
make
```
Any of the applications are run to ensure installation was succesful. 
```
./ptp4l
```
## IP Assignment ##
This server was configured for the DMZ of my home network 192.168.1.0/24, gateway on .254

```
sudo nano /etc/netplan/00-installer-config.yaml
```
Edit the file as shown

```
# This is the network config written by 'subiquity'
network:
  ethernets:
    eno1:
      dhcp4: no
      addresses:
        - 192.168.1.52/24
      routes:
        - to: default
          via: 192.168.1.254
      nameservers:
        addresses:
          - 9.9.9.9
          - 8.8.8.8
    eno2:
      dhcp4: true
    enp10s0f0:
      dhcp4: true
    enp10s0f1:
      dhcp4: true
  version: 2
```

## Test the card ##
Many of the examples on line require a rebuild of the kernel etc. This should not be required with UB2204. Test that the card is recognized using 

```
modprobe ptp_ocp
sudo dmesg | grep ocp
```
You should get a result as shown.

![output](ptp_ocp.PNG)
