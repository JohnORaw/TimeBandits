# Operating pi-ptp51
Check connectivity using ping, then run the command
```
sudo ptp4l -f ptp.config -m -q -s
```
It settles down after >20s
```
ptp4l[11353.542]: master offset        -83 s2 freq   +3795 path delay      2620
ptp4l[11354.542]: master offset        -10 s2 freq   +3843 path delay      2620
ptp4l[11355.542]: master offset        -65 s2 freq   +3785 path delay      2620
ptp4l[11356.542]: master offset         77 s2 freq   +3908 path delay      2620
ptp
```
