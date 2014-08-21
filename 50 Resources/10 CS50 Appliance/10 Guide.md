* First, you need a hypervisor to be able to run Virtual Machines. For this purpose, download and install VirtualBox. The download page is [here (click)](https://www.virtualbox.org/wiki/Downloads) and select either the **Windows x86**, **OS X x86**, or **Linux x86** version.

* Next, we'll download our Virtual Machine, which is called **CS50 Appliance 19**, by clicking [here](http://mirror.cs50.net/appliance50/19/i386/appliance50-19-vbox.ova). This file is over 1 Gigabyte in size, so it might take a while to download.

* When done downloading, open up **VirtualBox** and select **Import Appliance** (Appliance importeren). Select the `.ova` file you downloaded in the previous step. If VirtualBox prompts you for any settings, leave all of them to their default values.

* When succesful, you should now have a **CS50 Appliance 19** button on the left-hand side of your VirtualBox window. Go ahead and launch the appliance by double clicking its entry.

* Once fully booted, you should be on a similar desktop environment as you'd find in Windows or OS X. Try to make your VirtualBox go full-screen. If that works out just fine, you're done with these instructions and can start working on problem set 1. If it won't go fullscreen, or if it has very large borders around the desktop environment, continue with the steps below to enable full-screen on your VirtualBox.

* In VirtualBox's menu of the appliance (not within the appliance itself) select **Devices** (Apparaten) and then **Install guest additions** (Guest additions installeren). A disk icon should appear on your desktop within the appliance. Don't click that icon, but instead go to **Menu**, select **Programming**, and then **Terminal**. Within the terminal, type the following lines:

		sudo mount /dev/sr0 /media/
		sudo /media/VBoxLinuxAdditions.run

  This will take a little while to complete. After it is done (which you can verify by the text `jharvard@localhost (~):` reappearing), type the following:

		sudo umount /media/

  Finally, go to the **Devices** (Apparaten) menu of VirtualBox again and select **CD/DVD Devices > Remove disk from virtual drive**.

* Go to **menu** and fully shut down the appliance. Then restart it as in step 4. You should notice that the appliance will now go full-screen and that you can freely move your mouse from both within the appliance and outside of it, without having to "capture and release it". If any of these is not the case, call an assistant for help!