archfix
=======

my personal Arch Linux Installation script

Sumary code
sudo pacman –Syu
sudo pacman –S bash-completion
sudo pacman -S xorg-server xorg-xinit xorg-utils xorg-server-utils mesa
pacman  -S  xf86-video-intel
startx
pacman -S cinnamon
pacman –S net-tools
pacman -S network-manager-applet
ip link
systemctl stop dhcpcd@ens33.service
systemctl disable dhcpcd@ens33.service
systemctl stop dhcpcd.service
systemctl disable dhcpcd.service
pacman –S gdm
systemctl enable gdm
systemctl start gdm

About
=====
http://tuxomat.ml/my-arch-linux-instant-soup/

This tutorial guides you through transforming the main Arch Linux CLI only into a powerful and robust Desktop platform, with an awesome customizable desktop environment in Linux world this days – “Cinnamon” – and all the necessary software for an average desktop user, all of this done with the help of pacman software manager which does all necessary library, dependency and configuration checks on your behalf.

#Requirements

Previous Arch Linux installation on a Desktop, Laptop or Netbook with a working Internet connection.
Arch Linux Installation and Configuration Guide with Screenshots

Step 1: Install Xorg Server and Video Drivers

1. After initial system login we need to do a full system update by issuing the following command.

$ sudo pacman –Syu

2. Before we install all the necessary software’s, we need the help of a package “bash-completion“, that automatically completes commands or shows a list of possible commands by pressing TAB key.

$ sudo pacman –S bash-completion

3. The next step is to install the default X environment that provides the main Xorg server configurations and 3D support.

$ sudo pacman -S xorg-server xorg-xinit xorg-utils xorg-server-utils mesa


4. For an extra Xorg functionality also install the following packages.

$ sudo pacman -S xorg-twm xterm xorg-xclock

5. For ONLY a laptop or netbook, also install drivers for touchpad input support.

$ sudo pacman -S xf86-input-synaptics

6. Now we need to install system VGA (Video Card) specific drivers, but first of all we need to identify our system graphics. Issue the following command to identify your video card.

$ lspci | grep VGA

Check Video Card in Linux

If your system is a newer Laptop with Optimus support the output should show you two graphics card, usually an Intel and Nvidia or an Intel and ATI. The Linux drivers support for this kind of technology is now so brilliant at this time (you can try Bumblebee or Primus) for a minimal VGA switching.

7. After you detected your Graphics, is now time to install appropriate drivers. By default, Arch offers Vesa default video driver – xf86-video-vesa – that can handle a large number of graphic chipsets but does not provide any 2D or 3D acceleration support.

Also Arch Linux provides two types of Video Drivers.

Open Source (maintained and developed by distribution – recommended for installation).

Proprietary (developed and maintained by Video Cards manufacturer).

In order to list all available Open Source video drivers provided by Arch Linux official repositories run the following commands.

$ sudo pacman –Ss | grep xf86-video

List Open Source Video Drivers

To list Proprietary drivers run the following commands.
## Nvidia ##

$ sudo pacman –Ss | grep nvidia

## AMD/ATI ##

$ sudo pacman –Ss | grep ATI
$ sudo pacman –Ss | grep AMD

## Intel ##
$ sudo pacman –Ss | grep intel
$ sudo pacman –Ss | grep Intel

For Multilib Packages – 32-bit applications on Arch x86_64 – use the following commands.

## Nvidia ##
$ sudo pacman –Ss | grep lib32-nvidia
$ sudo pacman –Ss | grep lib32-nouveau

## ATI/AMD ##
$ sudo pacman –Ss | grep lib32-ati

## Intel ##
$ sudo pacman –Ss | grep lib32-intel
List Nvidia Drivers
List Nvidia Drivers

8. After you verify what drivers are available for your Graphics proceed with appropriate video driver package installation. As mentioned above you should stick to Open Source drivers, due to fact that they are maintained and properly tested by the community. To install Graphics Driver run the following command (after xf86-video – press TAB key to show list and autocomplete).

$ sudo pacman  -S  xf86-video-[TAB]your_graphic_card

Install Video Drivers in Arch Linux
Install Video Drivers

For further information regarding Xorg and Graphics drivers go to Arch Linux Wiki Xorg page at https://wiki.archlinux.org/index.php/Xorg.

9. After your Video Card appropriate drivers has been installed, is time to test Xorg server and video drivers by issuing the following command.

$ sudo startx

If everything is correctly configured a basic X session should start like in the screenshot below, which you can ditch by typing exit onto the larger console window.

$ exit

Start Basic X Session

#Step 2: Install Desktop Environment – Cinnamon

10. Now is time to provide an awesome innovative customizable Graphical User Interface – Full Desktop Environment for our system by installing Cinnamon package. Run the following command to install Cinnamon and other dependency from official arch repository.

$ sudo pacman -S cinnamon nemo-fileroller

11. Next step is to install GDM display manager package which helps system to start X server and provides a Graphical User Interface for users to login to Cinnamon DE.

$ sudo pacman –S gdm

12. Next step is to enable then start and test GDM by logging to Arch Linux using your credentials.

$ sudo systemctl enable gdm
$ sudo systemctl start gdm

13. After GDM loads you will be prompted with a Login window. Select your user -> click on Sign In left icon and choose Cinnamon, then enter your password and hit Sign In button or Enter key.
GDM Login Screen
GDM Login Screen

14. So far our internet connection is managed through command line, but if you want to manage your network connections from GUI you need to disable dhcpd service and install, enable and start Network Manager package. Also install net-tools package for extended network commands. From GUI open an UXterm shell prompt and run the following commands.
UXterm Terminal
UXterm Terminal

Install ifconfig provided by net-tools package and then view interface configuration using following commands.

$ sudo pacman –S net-tools
$ ifconfig

Next, install Network Manager.

$ sudo pacman -S network-manager-applet

Disable dhcpcd service.

$ sudo systemctl stop dhcpcd@ens33.service
$ sudo systemctl disable dhcpcd@ens33.service
$ sudo systemctl stop dhcpcd.service
$ sudo systemctl disable dhcpcd.service

Start end enable Network Manager.

$ sudo systemctl start NetworkManager
$ sudo systemctl enable NetworkManager

Start Network Manager
Start Network Manager
Disable dhcpd Service
Disable dhcpd Service
15. Now test your internet connection again running ifconfig to get network interfaces status, then issue a ping command against a domain.
Verify Network Connections
Verify Network Connections

To do a complete system testing, reboot your system to make sure everything is correctly installed and configured so far.

#Step 3: Install Basic Softwares

16. For now our system provides a minimum installed software that can’t be much of help on a day to day desktop or laptop use. Run the following long command to install basic softwares.

$ sudo pacman -S pulseaudio pulseaudio-alsa pavucontrol gnome-terminal firefox flashplugin vlc chromium unzip unrar 
p7zip pidgin skype deluge smplayer vlc audacious qmmp gimp xfburn thunderbird gedit gnome-system-monitor

Install Basic Softwares in Arch Linux
Install Basic Softwares

17. Also install codecs required for multimedia applications to encode or decode audio or video streams by issuing the following command.

$ sudo pacman -S a52dec faac faad2 flac jasper lame libdca libdv libmad libmpeg2 libtheora libvorbis libxv wavpack x264 xvidcore gstreamer0.10-plugins

18. Install LibreOffice package if you need Office tools like Writer, Calc, Impress, Draw, Math and Base by running the following command and press Enter key on selection (default=all).

$ sudo pacman -S libreoffice

Install LibreOffice 
Install LibreOffice

If you need other programs or utilities visit Arch Linux Packages page at https://www.archlinux.org/packages/, search for your package and install it via Pacman.
To remove a package use –R switch with pacman command.

$ sudo pacman -R package-to-remove

19. To install community maintained software install Yaourt Package Manager Tool (not recommended to use yaourt for beginner users).
$ sudo pacman -S yaourt

#Step 4: Customize Cinnamon Desktop

20. Cinnamon System Settings provides the interface through you can adjust and customize Arch and Cinnamon DE with whatever settings suits your needs. The following settings will show you how to change your system general look and feel (theme and icons). First of all, install Faenza Icon Theme and Numix Theme.

$ sudo pacman -S Faenza-icon-theme numix-themes
Install Faenza Icon Theme and Numix Theme
Install Faenza Icon Theme and Numix Theme

21. Then open System settings –> Themes –> Other Settings –> choose Numix on Controls and Window borders and
Faenza on Icons.
System Settings
System Settings
Theme Settings
Theme Settings

22. To change default Cinnamon theme go to System settings –> Themes –> Get more online –> select and install Minty, then go to Installed tab, choose and Apply Minty theme.
Install Minty Theme in Arch Linux
Install Minty Theme
Minty Theme Installed
Minty Theme Installed
That’s all! Now your final system appearance should look like in the screenshot below.
Cinnamon Desktop in Arch Linux
Cinnamon Desktop in Arch Linux

23. As a last customization to display a nice graphical monitoring tool on system toolbar first install the following packages.
$ sudo pacman -S libgtop networkmanager
Then open System Settings –> Applets –> Get more online, search for Multi-Core System Monitor and install it, then switch to Installed tab, right click and Add to panel.
Applets Panel
Applets Panel
Multi Core System Monitor
Multi Core System Monitor
Arch Linux System Monitoring
System Monitoring
Preferences Tab
Preferences Tab
You now have a complete good looking Arch Linux Desktop with basic software needed to browse Internet, watch movies, listen music or write Office docs.
For a complete Application List visit the following page
https://wiki.archlinux.org/index.php/List_of_applications
Build on a Rolling Release model Arch Linux also provides other Linux Desktop Environments, such as KDE, GNOME, Mate, LXDE, XFCE, Enlightenment, from its official repositories , so choosing Cinnamon or other DE is just a pure simple personal choice, but, in my opinion, Cinnamon provides a better flexibility (Themes, Applets, Desklets and Extensions) against complex customizations than its parent Gnome Shell.

#troubleshoot problems

1 Partition error
  a/ If you use USB boot for install Arch linux to another USB HDD. U must manual edit code in partition:
      HDD_NAME=/dev/sdXX
  b/ 
