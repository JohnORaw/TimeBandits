# KMNServer 
These are the build instruction for the time server KMNServer.

## Initial Setup
The hardware is a legacy Dell PE R520. The server was set to UEFI Boot and UB2204 was installed from a USB key. Updates were carried out.
```
sudo apt update
sudo apt upgrade -y
```

The latest version of LinuxPTP is downloaded.
```
wget https://sourceforge.net/projects/linuxptp/files/v3.1/linuxptp-3.1.1.tgz/download

```
Rename the download file and extract.
- x for extract
- v for verbose
- z for gnuzip
- f for file, should come at last just before file name.
```
mv download linuxptp-3.1.1.tgz
tar -xvzf ./linuxptp-3.1.1.tgz
```
Install **make** and **gcc**
```
sudo apt install make gcc
```
Change directory to linuxptp-3.1.1 and run **make**. This should build the current version of the application. Check for errors!
```
cd linuxptp-3.1.1/
make
```
Run any of the applications to ensure installation was succesful. 
```
./ptp4l
```