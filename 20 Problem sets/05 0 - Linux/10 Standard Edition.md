# Linux Intro


## Objectives

* Introduce the command line.
* Empower you to navigate through the filesystem and run programs from the command line.
* Have everything installed and ready to go for the following weeks.


## But first...

For the weeks to come you are going to be working in a version of Linux. Now hold your horses just yet, as we won't ask you to swap your operating system or create some kind of dual boot construction. Instead, you are going to be working in a virtual machine (the CS50 Appliance) while using a hypervisor (VMWare Workstation / Fusion). In this Appliance you can compile source code from lectures and implement problem sets yourself without having to figure out how to configure clang (a compiler), etc. Moveover, the CS50 Appliance lets you run Linux inside of a window on your own computer, even if you're already running Linux, Mac, or Windows.


## How to install?

### Windows / Linux

1. Download [VMWare Workstation 11](https://my.vmware.com/web/vmware/info/slug/desktop_end_user_computing/vmware_workstation/11_0).
2. Download the [CS50 Appliance](http://mirror.cs50.net/appliance50/2014/releases/29/appliance50-2014-vmware.ova).
3. Send an E-mail to help@mprog.nl and request a VMWare Workstation 11 key.
4. Follow instructions from step 3 [here](https://manual.cs50.net/appliance/2014/workstation/).

### Mac
1. Download [VMWare Fusion 7](https://my.vmware.com/web/vmware/info/slug/desktop_end_user_computing/vmware_fusion/7_0).
2. Download the [CS50 Appliance](http://mirror.cs50.net/appliance50/2014/releases/29/appliance50-2014-vmware.ova).
3. Send an E-mail to help@mprog.nl and request a VMWare Fusion 7 key.
4. Follow instructions from step 3 [here](https://manual.cs50.net/appliance/2014/fusion/).

If have trouble installing do not hesitate to ask for help!


## Lets boot

With everything installed, we are ready to go and boot the CS50 Appliance for the first time. So go ahead, run your version of VMWare and from there boot the CS50 Appliance. Booting the Appliance might take a minute or so, please be patient! You should end up on John Harvard's desktop.

If the Appliance feels unbearably slow you might need to enable [hardware virtualization](https://manual.cs50.net/virtualization). Even with hardware virtualization enabled, though, virtual machines might feel slow if you are using an older machine. Alternatively you can crank up your virtual machine by allowing it to use more than one processor core and more RAM. Simply exit the Appliance and reboot VMWare. You should now be on the screen where you can boot the Appliance, instead of doing so, click **Edit virtual machine settings**. Here you can change the innards of the virtual machine! Be wary of the specifications of your physical machine though!

If your Appliance is running in a small window even though you clicked the fullscreen button (one of the top buttons in VMWare). You might want to increase your resolution as by default the Appliance runs a resolution of 800x600! To do this, select **Menu** > **Settings Manager** > **Display** within the Appliance, select a new value to the right of resolution and press close.


## Dropbox

To reduce the risk of you losing important files, and hopefully lessen the dog-ate-my-homework arguments, we strongly urge you to use Dropbox. Dropbox is a cloud service that has you store and synchronize files, such that if your Computer or Appliance breaks down during the course or thereafter your important files are still stored somewhere within the cloud. To install Dropbox on the Appliance follow [these instructions](https://manual.cs50.net/appliance/2014/#how_to_enable_dropbox).


## This is the CS50 Appliance

Lets start exploring the Appliance a bit. In the taskbar you will find three pre installed programs: Gedit, Google Chrome, and the Terminal.

Go ahead and run Gedit. You will see it is just a text editor (think Notepad, not Microsoft Word). You will use Gedit in the weeks to come to do your coding. Gedit also supports a few cool features such as a build-in terminal and syntax highlighting.

Now run Google Chrome, which as you probably already know is an internet browser. If all is correct, you should be able to browse the web now. So go ahead and open this page within your Appliance.

Welcome back! Okay, now lets run the terminal. The terminal is a text based interface to your computer, instead of a graphic interface which you are most likely used to. Go ahead and enter a simple command: 

	echo "Hello, World!"

You should now see a new line with Hello, World! printed. The command that was executed was echo, which as you might have guessed echos its parameter which is "Hello, World!".


## We need to go deeper

### Running programs

Lets explore the terminal a bit more, lets try running Gedit from the terminal. Close Gedit if you still have it open, and enter in the terminal:

	gedit

Gedit should now have popped up, and should be all set to text edit. Now instead of running a simple command such as echo, we are running an entire graphical program from the terminal. But you should notice a slight difference when returning to the terminal. You can no longer issue new commands! This is because you are still running Gedit. So go ahead and close Gedit. You should now see that you are able to enter commands once again.

Okay, lets run some more programs. Just a hint before we continue, copy-paste within the terminal is ctrl+shift+c for copy and ctrl+shift+v for paste. Now enter or rather copy-paste in the terminal:

	google-chrome https://www.youtube.com/watch?v=rfh4Mhp-a6U

Just like before we issued a command (google-chrome), passed it an argument (the URL) and are now running a program (Google Chrome). If you already had Google Chrome open, you should see it created a new tab, rather than creating a new window. As such the terminal is not occupied and we can continue entering commands. If you did not have Google Chrome open beforehand, simply close it now. 


### Navigating

So you have seen how to run programs from the terminal. So now lets explore the linux file system from within the terminal. As the terminal is text based you cannot simply click your way through the directories as you might do under Windows or under Mac. Instead you have to enter commands to navigate your way through. First things first, you should see the following line in the terminal:

	jharvard@appliance (~):

What this means is that you are on John Harvards desktop in the home directory (the ~). Now enter the following command:

	ls

You should see a new line printed with a list (ls = LiSt) of all the directories (in blue) and files (in white) within your home directory. Time to leave base, lets go to your Dropbox directory, which should be in the list printed by ls. If not, go back and install Dropbox! Now enter the command:

	cd Dropbox

You should now see a small change, namely ~ changed to ~/Dropbox. This essentially means you are now within the Dropbox directory which parent is the Home directory. So you changed your directory (cd = Change Directory) to Dropbox. Now lets head back. Enter the following command:

	cd ..

Here you used the change directory command to move to the .. directory, which is simply the parent directory. Hence, you are now back in the home directory again as this was the parent of the Dropbox directory. There are multiple ways to go to the home directory: cd, and cd ~ both work. Okay, back to the Dropbox folder. Getting tired of typing? Try the following, press tab once after entering the following:

	cd Dr

You should see that the terminal auto completes the directory name. This only works if there are no files which start with Dr in this directory. If there are files which start with Dr the terminal will auto-complete as far as it can, and leave the choice which directory or file to pick to the user, that is you. To see which directories or files the terminal is unsure about in such a case you can hit tab twice.

### Creating