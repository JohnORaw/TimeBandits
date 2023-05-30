The second was originally defined as 1/86400 of a mean solar day as determined by the rotation of the Earth around its axis and around the Sun. 
However, as a basis for current accuracy requirements, the rotation of the Earth does not provide a uniform time standard. 

Generally, the Earth’s rotation will slow due to tidal interaction, primarily with the moon. The solar day becomes c. 1.7ms longer every century due mainly to tidal friction. 

From 1967, the second was redefined as the SI-Second, the duration of 9,192,631,770 periods of radiation corresponding to transitions between two ground states of Caesium 133. Coordinated Universal Time (UTC) is based on TIA, offset by an integer number of seconds. 

As of 1st January 2017, TAI was 37 seconds ahead of UTC. It represents the time of day at the prime meridian, Greenwich, UK.
UT1 is Mean Solar Time and whenever UTC ≠ UT1 by > 0.6 second as determined by the International Earth Rotation 
and Reference Systems Service (IERS).

A leap second is inserted to bring clocks back in line with reality, either on June 30th or December 31st of that year. 
Leap seconds are announced by the IERS in its [Bulletin C.](https://www.iers.org/IERS/EN/Publications/Bulletins/bulletins.html) 
For computational purposes, a standard file [leap-seconds.list](ftp://ftp.boulder.nist.gov/pub/time/leap-seconds.list) is used by Linux time services.

In Linux, the following command downloads this list.
```
wget ftp://ftp.boulder.nist.gov/pub/time/leap-seconds.list
```
To adjust PHC Clock for difference between UTC and TAI (currently 37 seconds), the phc_ctl command is used.
```
sudo phc_ctl eth0 "set;" adj 37
```
The ouput should be something like
```
phc_ctl[392.928]: set clock time to 1685449352.745774672 or Tue May 30 13:22:32 2023
phc_ctl[392.930]: adjusted clock by 37.000000 seconds
```

