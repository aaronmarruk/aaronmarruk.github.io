---
title:  "Installing Solus OS on a Macbook Air"
date:   2018-10-06 10:18:00
description: A quick guide to getting Solus OS running on a Macbook Air.
---

This is a simple step-by-step guide for installing Solus OS as the main operating system on a Macbook Air 11 inch (Mid 2014). 

### Step 1: Download the Solus ISO

The first thing you will need to do is download the Solus ISO. You can [download Solus OS here](https://getsol.us/download/). 

Solus is available in a few different flavours. In this guide I'm installing the Budgie version, but may be able to follow along with either the GNOME or MATE version.

### Step 2: Create a boot-able USB

Once you have downloaded your preferred Solus flavour, you will need to create a boot-able USB drive. This will be used to install Solus onto your Mac. I recommend using Etcher for this, which is a free tool for creating boot-able USB drives. Download etcher from [the Etcher website](https://etcher.io/)

Open etcher and the select the Solus ISO file which you downloaded earlier. Insert your USB drive into your mac – you will need a USB drive with at least 2GB storage. Next, select the USB drive as the target, then select "flash". The flashing process should take a few moments.

### Step 3: Reformat the SSD

I’ve chosen to install Solus as the main operating system on my Macbook. I initially had a bit of trouble formatting my Mac’s SSD using MS-FAT (FAT32). In Disk Utility I noticed that it’s not possible to set MS-FAT as the primary partition format (at least to my knowledge). I found a workaround for this using recovery mode.

### Step 3a: Boot into recovery mode

Restart the Mac and hold `CMD + R`. This will boot the machine into recovery mode, which could take a minute or two.

### Step 3b: format the disk

Once in recovery mode, select the disc you want to format, and then select “erase”, making sure to select MS-FAT as the partition-type. MS-FAT (FAT32) is the required partition format for Solus OS.

### Step 4: Boot into the USB

Once your hard drive has been formatted correctly, restart the machine holding `ALT` to enter the boot menu. 

### Step 5: Set kernel parameters

This next step is required in order for Solus to be able to see your Mac’s internal SSD. 

Once the boot loader screen appears (you should see a black screen with the text “Solus OS 3.9999” or similar) press the “E” key. This will display a long editable string of text, containing kernel parameters. We will set a new parameter so that Solus can see your Mac’s SSD. At the end of the line of text enter `intel_iommu=off` and then select `Solus 3.9999` to start booting into the USB drive.

### Step 6: Install Solus

Once booted into the USB, select “Install Solus” from the desktop. If step 5 was completed successfully you should see the Mac's SSD when prompted by the installer.

Once the installation has finished you should restart your machine. At this point you will have to add the kernel parameter once more on boot. This time, hold SPACE until the boot menu appears and then add the parameter as you did in step 5. Once the machine boots into Solus we will make this change permanent.

### Step 7: Permanently set kernel parameters

As you've seen, we've been setting the kernel parameter each time we start the Macbook. We can do better than this by adding the new parameter directly to the boot manager so that it's always available.

```
sudo su
mkdir -p /etc/kernel
echo "intel_iommu=off" > /etc/kernel/cmdline
clr-boot-manager update
exit
```

### Step 8: Install WiFi adapter

Most things seem to be working out of the box. One thing that doesn’t work, is WiFi. To fix this issue you will need to update some drivers, which will require having an internet connection. I tethered my phone over Bluetooth and connected to the internet using my phone's WiFi connection.

In Android, go to settings -> network -> tethering and then select Bluetooth tethering. Connect to your phone in Solus by going to settings -> Bluetooth, and selecting your phone from the list of connections. Once connected, your phone’s network should appear in the network setting tab.

Once you have a connection, you can go ahead and install the driver. Open Terminal and run:

```
sudo -i
eopkg install broadcom-sta-current 
echo 'install wl /sbin/modprobe cfg80211; /sbin/insmod /lib/modules/$(/bin/uname -r)/kernel/drivers/net/wireless/wl.ko' > /etc/modprobe.d/wl.conf 
echo wl > /etc/modules-load.d/wl.conf 
modprobe wl
exit
```

Restart your Mac. Once Solus has started you should be able to connect to the internet using your network adapter by going to settings -> WiFi and selecting your network. 

### Step 9: Fan noise

Pretty much straight away I noticed my Mac's fans we making a huge amount of noise, even when the machine was idle. This is a pretty common problem when running Linux on Mac hardware. 

I fixed this issue with the help of an interesting bit of software which can be [downloaded from Github](https://github.com/dgraziotin/mbpfan).

Simply clone the above repo and then cd into the directory in your Downloads folder. Run "sudo make" followed by "sudo make install" to build/install the software. To run the software run "sudo mbpfan." 

You should really check out the README for the repo to get a good idea as to how the software works, and for more detailed usage instructions.

### Step 10: enjoy

I hope this has provided you with a quick reference for getting Solus OS running on your Mac hardware. If you have any questions or pointers I would love to hear them. Thanks!
