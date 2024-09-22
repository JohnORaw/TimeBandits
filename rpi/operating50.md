# Operating pi-ptp50
Create a ptp.config file to define any common parameters. If the GNSS is connected via USB, the device name may be /dev/ttyACM0

/dev/ttyAMA0 in the example below is UART No.2 connected to pins 8 (TX) and 10 (RX) on the CM4 J8 GPIO. 

The leap-seconds file must be in the same directory if running ts2phc from the command line. The leap-seconds file can also be found here in the tzdata apt package and is stored locally here: /usr/share/zoneinfo/leap-seconds.list. 

```
[global]
ts2phc.nmea_serialport /dev/ttyAMA0
leapfile leap-seconds.list
tx_timestamp_timeout 100
[eth0]
```
Synchronize the PTP hardware clock from the GNSS, verify. Open an SSH window and run as shown.
```
sudo ts2phc -f ptp.config -s nmea -m -q -l 7
```
The master offset settles down over time.

```
ts2phc[72.332]: eth0 extts index 0 at 1685452383.999999997 corr 0 src 1685452384.935373093 diff -3
ts2phc[72.332]: eth0 master offset         -3 s2 freq   -2261
ts2phc[73.340]: nmea delay: 142607833 ns
ts2phc[73.340]: eth0 extts index 0 at 1685452385.000000001 corr 0 src 1685452385.943398734 diff 1
ts2phc[73.340]: eth0 master offset          1 s2 freq   -2258
ts2phc[73.400]: nmea sentence: GNRMC,131228.00,A,5510.00075,N,00726.09158,W,0.008,,300523,,,A,V
ts2phc[74.348]: nmea delay: 145597639 ns
```
Once this is working, open a different SSH window 
```
sudo ptp4l -f ptp.config -m -q
```
The Grand Master is now operating on the local LAN.

# Start ts2phc service

### Create the ts2phc.service file
Note, you do need to use restart as the service takes time to start after the NIC comes up. 

```
pi@cm4:~ $ cat /etc/systemd/system/ts2phc.service
[Unit]
Description=Synchronize one or more PTP Hardware Clocks using external time stamps
Documentation=man:ts2phc
After=network.target

[Service]
Type=simple
Restart=always
RestartSec=1
ExecStart=/usr/sbin/ts2phc -f /etc/linuxptp/ptp.config -s nmea -m -q -l 7

[Install]
WantedBy=multi-user.target
```

### Start service
pi@cm4:~ $ systemctl start ts2phc

## Check it is working and logging
```
pi@cm4:~ $ systemctl status ts2phc
● ts2phc.service - Synchronize one or more PTP Hardware Clocks using external time stamps
     Loaded: loaded (/etc/systemd/system/ts2phc.service; enabled; preset: enabled)
     Active: active (running) since Sun 2024-06-23 19:45:51 IST; 26min ago
       Docs: man:ts2phc
   Main PID: 798 (ts2phc)
      Tasks: 2 (limit: 448)
        CPU: 2.660s
     CGroup: /system.slice/ts2phc.service
             └─798 /usr/sbin/ts2phc -f /etc/linuxptp/configs/local-gps.cfg -s nmea -m -q -l 7

Jun 23 20:12:15 cm4 ts2phc[798]: ts2phc[1600.452]: eth0 master offset          3 s2 freq    +281
Jun 23 20:12:15 cm4 ts2phc[798]: ts2phc[1600.501]: nmea sentence: GNGGA,191215.00,5317.77337,N,00616.79178,W,1,09,1.03,57.4,M,52.9,M,,
Jun 23 20:12:15 cm4 ts2phc[798]: ts2phc[1600.551]: nmea sentence: GNGSA,A,3,13,09,20,29,05,,,,,,,,1.73,1.03,1.39
Jun 23 20:12:15 cm4 ts2phc[798]: ts2phc[1600.601]: nmea sentence: GNGSA,A,3,65,81,87,88,,,,,,,,,1.73,1.03,1.39
Jun 23 20:12:15 cm4 ts2phc[798]: ts2phc[1600.667]: nmea sentence: GPGSV,4,1,13,05,50,297,26,06,07,184,,07,58,084,,09,27,078,10
```
### Enable ts2phc to start on reboot
```
root@cm4:/home/pi# systemctl enable ts2phc
Created symlink /etc/systemd/system/multi-user.target.wants/ts2phc.service → /etc/systemd/system/ts2phc.service.
root@cm4:/home/pi#
```
Reboot and check that the service is working after a reboot. 




