#### [GUIDE]How To Add Wifi Drivers in Android NetHunter Kernel
`Mominul Islam Hemal`

Kali NetHunter is a free and open-source mobile penetration testing platform for Android devices, based on Kali Linux. Kali NetHunter is available for un-rooted devices, for rooted devices that have a custom recovery, and for rooted devices with custom recovery for which a NetHunter specific kernel is available. 
#### `Here is our workplan`:
```sh
├── Apply frame injection patch
├── Remove Unnecessary files
├── Add Wifi Drivers 
├── Compile & Fix Errors 
```     
#### `STEP-2:` Remove Unnecessary Files

1.We have to remove the original RTL8188EU drivers from the kernel source.(if we want to add `RTL8188EUS` as inbuilt,not as module)
- Go to `kernel_directory/drivers/staging` folder.For example: `fenix` is my kernel_directory.

`rm -r rtl8188eu`

- Now, We will edit `Makefile` and `Kconfig` of `staging` directory.

Search this line and delete it from the file and save .

`obj-$(CONFIG_R8188EU) += rtl8188eu/`

<p align="center"><img src="https://raw.githubusercontent.com/CaliBerrr/LinuxArchive/main/image/IMG_20210102_235214-01.jpeg" width="500"/></p>

Remove it
Now comes the part of editing Kconfig file .To edit Kconfig, Give this Command in the present directory.

nano Kconfig
Search this line and delete it from the file and save .

```sh
source "drivers/staging/rtl8188eu/Kconfig"
```

<p align="center"><img src="https://raw.githubusercontent.com/CaliBerrr/LinuxArchive/main/image/IMG_20210102_235147-01.jpeg" width="500"/></p>

Remove from Kconfig
STEP-2:Add Kimcoders Aircrack RTL8188eus driver

a)Go to `kernel_directory/Drivers folder`.Git clone the drivers in kernel source using below command.
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
<p align="center"><img src="https://raw.githubusercontent.com/CaliBerrr/LinuxArchive/main/image/IMG_20210102_235118-01.jpeg" width="500"/></p>
                        
Add in Makefile
Now add this line in Kconfig File and save it.

```
#Aircrack drivers

source "drivers/rtl8188eus/Kconfig"

source "drivers/rtl8812au/Kconfig"

```

<p align="center"><img src="https://raw.githubusercontent.com/CaliBerrr/LinuxArchive/main/image/IMG_20210102_235040-01.jpeg" width="500"/></p>

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


