# Forensics
An assignment for my Introduction to Ethical Hacking course at UMD.

## Part 1

>1. What kind of device took the photo? What specifics can you ascertain about it (the device), and why might they be relevant?

After running ```exiftool imagefun.jpg``` I was able to reveal the device that took the photo, it was an Apple Iphone 4S, this was revealed as the Camera Model Name. Some other interesting things about this device is that it stores its data in Big Endian, which tells us how memory addresses are stored on this device and could possibly be used to exploit the device. 

Another interesting thing is the software version ```iCamera 1.2.3 last-update=2014```. Having knowledge of the software version and the last year it was updated allows us to find exploits and vulnerabilities in the devices operating system. 

>2. When and where was the photo taken? Why might this be relevant?

The GPS position was given in terms of longitude and latitude:

```
Longitude: 38 deg 55' 1.41" N
Latitude: 77 deg 1' 42.81" W
```
Using Google Maps, I inputed these coordinates and got the address to be:

``` 1207-1209 U Street NW, Washinton DC, 20009```

Using google street view, it does not seem at all like the setting in which the picture was taken... odd.

As for the time of the phone taken, both the Original Date and Time and the Created Date indicate that the photo was taken on January 1st, 1984 at 12:12:12, which is alittle fishy due to the fact that the Iphone 4S was not around during 1984, this looks like someone could have fabricated this date.

>3. Find the flag(s) hidden in the photo.

So my thought process through this part went like this:

1. Run exiftool to see if that would reveal any information, but all it gave me was trash data. 
2. Attempted to run binwalk on the imagefun.jpg inorder to discover more information, did not reveal much.
3. Finally I attempted to use steganography inorder to reveal any encrypted information, if it existed within the image, so I ran this command as seen in the lecture slides: 

```steghide extract -sf imagefun.jpg -xf out.txt```
I was then prompted to enter a passphrase, now I knew that I was on the right track!

I tried various passwords that have come up in assignments before such as:
password, blink182, briong70, and finally mnthomp22 which was accepted and I was able capture the flag:

```
congrats, you made it here!
your flag: CMSC389R-{m4rk's b4d s3cur1ty}
```

