#### [GUIDE]How To Add Wifi Drivers in Android NetHunter Kernel(RTL8188EUS,RTL8812AU)
`Mominul Islam Hemal`

Kali NetHunter is a free and open-source mobile penetration testing platform for Android devices, based on Kali Linux. Kali NetHunter is available for un-rooted devices, for rooted devices that have a custom recovery, and for rooted devices with custom recovery for which a NetHunter specific kernel is available. 

#### `STEP-1:` Removing Unnecessary Files

1.At first we have to remove the original RTL8188EU drivers from the kernel source(Only for V4.14 and upper version kernel.Skip it if your kernel is lower than v4).

For this follow these steps:

a) Go to `yourkernel_directory/drivers/staging` folder.Now run this command.It will remove rtl8188eu driver folder that may collide with our driver.

`rm -r rtl8188eu`

b) Now, We will edit Makefile and Kconfig of staging directory.

Search this line and delete it from the file and save .

`obj-$(CONFIG_R8188EU) += rtl8188eu/`

<p align="center"><img src="image/IMG_20210102_235214-01.jpeg"></img></p>


Remove it
Now comes the part of editing Kconfig file .To edit Kconfig, Give this Command in the present directory.

nano Kconfig
Search this line and delete it from the file and save .

`source "drivers/staging/rtl8188eu/Kconfig"`

<p align="center"><img src="image/IMG_20210102_235147-01.jpeg"></img></p>

Remove from Kconfig
STEP-2:Add Kimcoders Aircrack RTL8188eus driver

a)Go to `yourkernel_directory/Drivers folder`.Git clone the drivers in kernel source using below command.
```sh
#rtl8188eus driver
git clone --depth=1 https://github.com/aircrack-ng/rtl8188eus -b v5.3.9

#rtl8812au driver
git clone --depth=1 https://github.com/aircrack-ng/rtl8812au -b v5.6.4.2
```
b)We have to add two lines in Makefile and Kconfig in drivers folder.

first we will edit the Makefile.Editing command is same as it was before.

Add this line in Makefile and save it.

```
#Aircrack drivers
obj-$(CONFIG_RTL8188EU) += rtl8188eus/
obj-$(CONFIG_88XXAU)    += rtl8812au/
```
<p align="center"><img src="image/IMG_20210102_235118-01.jpeg"></img></p>
                        
Add in Makefile
Now add this line in Kconfig File and save it.

```
#Aircrack drivers

source "drivers/rtl8188eus/Kconfig"

source "drivers/rtl8812au/Kconfig"

```

<p align="center"><img src="image/IMG_20210102_235040-01.jpeg"></img></p>

Add in Kconfig
We have Successfully Added the driver in our source.

STEP-3:SELECT THE DRIVER AND COMPILE.

We have to select this driver from menuconfig .Execute `make menuconfig` and wait a sec.Navigate to `device drivers` and select the marked option.



Select it
Now save it and Compile the kernel.Hurrah,You have Added RTL8188EUS driver in your kernel.

NOTE: it might not work with all kernel as some users reported not to working with their kernel.But it worked for my all devices.You Can give it a try.



TESTING THE KIMOCODER'S AIRCRACK DRIVER:

Worked for me. monitor mode and injection working.


Test-1


