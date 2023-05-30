# GNSS Configuration
The original testing for this project was with an Ardusimple UBX ZED R9P, left over from a navigation project.
This version uses a GNSS OEM GNSS OEM ELT0113, it can be configured using a standard USB cable and U-Center Software.

For this project, UART2 was used with the following configuration changes.

1. Baud rate set to 9600
2. Only GNRMC egress from UARTs

