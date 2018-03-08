# Forensics
An assignment for my Introduction to Ethical Hacking course at UMD.

## Part 1

>1. What kind of device took the photo? What specifics can you ascertain about it (the device), and why might they be relevant?

Ouput of running ```exiftool imagefun.jpg```:

![alt text]()
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

## Part 2

>1. What kind of system was the program built for? (e.g., OS, libc version, compiler version)

The first thing I did was to run the strings command on the core dump to simply get a glimpse of what was in this program, I ran this command: 

```strings fubar.core```

This outputed a long list of mostly garbage data with some exceptions... for example I found the operating system, libc version, and compiler version on one line: 

```GCC: (Ubuntu 5.4.0-6ubuntu1~16.04.9) 5.4.0 20160609```

along with some other interesting data...

```MNTHOMP_PASSWORD=ilovenickelback```
```you should run: sudo gcore -o fubar 3847 (students ignore this)```
```dMark Thompson (You're on the right track if you find this - keep digging class!) <mnthomp22@tuta.io>```
```EN=true```

>2. What arguments was the program run with?

The program was not run with any arguments, I found this by running strings again, but this time searching for ```./fubar``` using this command:

```strings fubar.core | grep "./fubar"```

This revealed that fubar was run without any arguments, but simply like this:

```./fubar```


>3. What was in the program's environment when it was dumped?

As discovered in my earlier run of ```strings fubar.core```, there were some local data present in the environment, such as:

```MNTHOMP_PASSWORD=ilovenickelback```
```PGP_HIDDEN=true```
```EN=true```


>4. Is there any data embedded in the program? If so, what is it?


## Part 3


>1. What was the domain requested in the HTTP request, and what IP did it resolve to?

So while following along with the forensics video and the live Wireshark demo, I opened traffic.pcap in Wireshark and searched for all http requests. A certain address that showed up was ```129.2.94.135``` after running shodan it was revealed that the address resolved to:

```irc.csec.umiacs.umd.edu```

I then tried to log onto ```irc.csec.umiacs.umd.edu/mnthomp_beedogs.html```, but I was greeted with a 404 error. I continued following the directions of the Forensics live demo and exported all objects as HTTP files, and this way I was able to reconstruct Mark's beedogs page. 

![alt text](https://github.com/yreiss1/Forensics/blob/master/mnthomp_beedogs.png)


