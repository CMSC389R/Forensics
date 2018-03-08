# Forensics
An assignment for my Introduction to Ethical Hacking course at UMD.

## Part 1

>1. What kind of device took the photo? What specifics can you ascertain about it (the device), and why might they be relevant?

After running ```exiftool imagefun.jpg``` I was able to reveal the device that took the photo, it was an Apple Iphone 4S, this was revealed as the Camera Model Name. Some other interesting things about this device is that it stores its data in Big Endian, which tells us how memory addresses are stored on this device and could possibly be used to exploit the device. 

Another interesting thing is the software version ```iCamera 1.2.3 last-update=2014```. Having knowledge of the software version and the last year it was updated allows us to find exploits and vulnerabilities in the devices operating system. 

>2. When and where was the photo taken? Why might this be relevant?

