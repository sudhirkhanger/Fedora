# Personal Fedora Notes

## Google Chrome
 
[Chrome](https://www.google.com/intl/en_in/chrome/browser/)
 
[Hangouts Plugin](https://www.google.com/tools/dlpage/hangoutplugin)

## RPM Fusion

[RPMFusion](http://rpmfusion.org/Configuration)

## Java

### OpenJDK 8

	sudo yum install java-1.8.0-openjdk.x86_64 icedtea-web.x86_64


### Oracle Java 8

#### Install

	sudo su
	rpm -ivh jdk-8u25-linux-x64.rpm

#### Upgrade
  
	rpm -Uvh jdk-8u25-linux-x64.rpm

#### Setup environmental variables

	emacs -nw .bashrc
	
	export JAVA_HOME=/usr/java/default/
	export PATH=$JAVA_HOME/bin:$PATH
  
#### Set Alternatives

	alternatives --install /usr/bin/java java /usr/java/default/jre/bin/java 200000
	alternatives --install /usr/bin/javaws javaws /usr/java/default/jre/bin/javaws 200000
	alternatives --install /usr/lib64/mozilla/plugins/libjavaplugin.so libjavaplugin.so.x86_64 /usr/java/default/jre/lib/amd64/libnpjp2.so 200000
	alternatives --install /usr/bin/javac javac /usr/java/default/bin/javac 200000
	alternatives --install /usr/bin/jar jar /usr/java/default/bin/jar 200000

	alternatives --config java
	alternatives --config javaws
	alternatives --config libjavaplugin.so.x86_64
	alternatives --config javac
	alternatives --config jar


[Oracle Docs](http://docs.oracle.com/javase/7/docs/webnotes/install/linux/linux-jdk.html#install-64-rpm)

[if-not-true-then-false.com](http://www.if-not-true-then-false.com/2010/install-sun-oracle-java-jdk-jre-7-on-fedora-centos-red-hat-rhel/)

[Fedora Forums](http://forums.fedoraforum.org/showthread.php?t=297016)

[John Goltzer Blogspot](http://johnglotzer.blogspot.in/2012/09/alternatives-install-gets-stuck-failed.html)

### Android

#### Android SDK Dependencies

	sudo yum install glibc.i686 glibc-devel.i686 libstdc++.i686 zlib-devel.i686 \
	ncurses-devel.i686 libX11-devel.i686 libXrender.i686 libXrandr.i686 \
	mesa-libGL.i686

#### Android Build Dependencies

	sudo yum install gcc gcc-c++ gperf flex bison glibc-devel.{x86_64,i686} \
	zlib-devel.{x86_64,i686} ncurses-devel.i686 readline-devel.i686 perl-Switch

#### Android SDK Environmental Variable

	~/.bashrc
  
	PATH=$PATH:$HOME/AndroidSDK:$HOME/AndroidSDK/tools
	export PATH

    # For SDK version r_08 and higher, also add this for adb:
	PATH=$PATH:$HOME/AndroidSDK/platform-tools
	export PATH

#### udev Rules

	cd /etc/udev/rules.d
	wget https://raw.githubusercontent.com/M0Rf30/android-udev-rules/master/51-android.rules
	chmod a+r /etc/udev/rules.d/51-android.rules
  
[Fedora Wiki HOWTO_Setup_Android_Development](https://fedoraproject.org/wiki/HOWTO_Setup_Android_Development)

[Using Hardware Devices](http://developer.android.com/tools/device.html)

[MORf30 Github](https://github.com/M0Rf30/android-udev-rules/blob/master/51-android.rules)

### Thinkfan
---------

#### Install and enable systemd file

	sudo yum install thinkfan
	sudo systemctl enable thinkfan

#### Modify config and add output of following command to it prefixing with ``sensors``

	find /sys/devices -type f -name "temp*_input"
  
	/etc/thinkfan.conf
    ---------------------------------------------------------------
	sensor /sys/devices/virtual/hwmon/hwmon0/temp1_input
	sensor /sys/devices/platform/coretemp.0/hwmon/hwmon2/temp3_input
	sensor /sys/devices/platform/coretemp.0/hwmon/hwmon2/temp1_input
	sensor /sys/devices/platform/coretemp.0/hwmon/hwmon2/temp2_input
  

## Media Codecs

    sudo yum install -y amrnb amrwb faac faad2 flac gstreamer1-libav gstreamer1-plugins-bad-freeworld gstreamer1-plugins-ugly \
    gstreamer-ffmpeg gstreamer-plugins-bad-nonfree gstreamer-plugins-espeak gstreamer-plugins-fc gstreamer-plugins-ugly \
    gstreamer-rtsp lame libdca libmad libmatroska x264 xvidcore gstreamer1-plugins-bad-free gstreamer1-plugins-base \
    gstreamer1-plugins-good gstreamer-plugins-bad gstreamer-plugins-bad-free gstreamer-plugins-base gstreamer-plugins-good
    
[Fedy](https://github.com/satya164/fedy/blob/master/plugins/util/media_codecs.sh)

## Bumblebee

    yum install libbsd-devel libbsd glibc-devel libX11-devel help2man autoconf git tar glib2 glib2-devel kernel-devel \
    kernel-headers automake gcc gtk2-devel VirtualGL VirtualGL.i686
    yum install http://install.linux.ncsu.edu/pub/yum/itecs/public/bumblebee/fedora22/noarch/bumblebee-release-1.2-1.noarch.rpm
    yum install bbswitch bumblebee
    yum install http://install.linux.ncsu.edu/pub/yum/itecs/public/bumblebee-nonfree/fedora22/noarch/bumblebee-nonfree-release-1.2-1.noarch.rpm
    yum install bumblebee-nvidia primus primus.i686

## ksuperkey

### Installation

    sudo yum install git gcc make libX11-devel libXtst-devel pkgconfig
    git clone https://github.com/hanschen/ksuperkey.git
    cd ksuperkey
    make
    sudo make install
    
### Autostart

    ksuperkey -e 'Super_L=Alt_L|F2'
    

[Github hanschen](https://github.com/hanschen/ksuperkey)

### TLP

#### Configure Repo

	dnf install http://repo.linrunner.de/fedora/tlp/repos/releases/tlp-release-1.0-0.noarch.rpm
	dnf install http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-stable.noarch.rpm

#### Installation

	sudo yum install tlp tlp-rdw akmod-tp_smapi akmod-acpi_call kernel-devel

[Linrunner.de](http://linrunner.de/en/tlp/docs/tlp-linux-advanced-power-management.html#installation)


### VirtualBox

	dnf install akmod-virtualbox virtualbox dkms
	usermod -a -G vboxusers $USER
	systemctl enable dkms

### HandBrake 

[Negativo17](http://negativo17.org/handbrake/)

### Skype

[Negativo17](http://negativo17.org/skype-and-skype-pidgin-plugin/)

### RedShift Plasma Widget

	sudo dnf install redshift-gtk

### Gnome Encfs Manager

	cd /etc/yum.repos.d/
	wget http://download.opensuse.org/repositories/home:moritzmolch:gencfsm/Fedora_20/home:moritzmolch:gencfsm.repo
	dnf install gnome-encfs-manager

[Project Homepage](http://www.libertyzero.com/GEncfsM/)

[OBS mortizmolch](http://software.opensuse.org/download.html?project=home:moritzmolch:gencfsm&package=gnome-encfs-manager)

### Genymotion

	./genymotion-2.2.1_x64.bin


### SoundKonverter

[Github HessiJames](https://github.com/HessiJames/soundkonverter/wiki/Installing-soundKonverter#precompiled_packages)

### reStructuredText

	sudo dnf install python-docutils python-sphinx
  
### Microsoft Core Fonts

    sudo yum install msttcore-fonts-installer-2.6-1.noarch.rpm
    
[mscorefonts2 Sourceforge](http://sourceforge.net/projects/mscorefonts2/?source=typ_redirect)

### Speed up LibreOffice

- Undo steps 20 or 30 steps
- Under Graphics cache, set Use for LibreOffice to 128 MB
- Set Memory per object to 20 MB (up from the default 5 MB).

### wmsystemtray

	yum install wmsystemtray
  
#### KWin Rules

	[Application settings for wmsystemtray]
	Description=Application settings for wmsystemtray
	desktop=-1
	desktoprule=2
	noborder=true
	noborderrule=2
	skippager=true
	skippagerrule=2
	skipswitcher=true
	skipswitcherrule=2
	skiptaskbar=true
	skiptaskbarrule=2
	type=2
	typerule=2
	wmclass=wmsystemtray0 wmsystemtray
	wmclasscomplete=true
	wmclassmatch=1

#### Further tweaking

- Uncheck Arrangement & Access > Skip Taskbar
- Appearance & Fixes > Window Type > Force > Normal
  
#### Autostart

	wmsystemtray --non-wmaker --bgcolor white

[Where Are My Systray Icons?](http://blog.martin-graesslin.com/blog/2014/06/where-are-my-systray-icons/)

[How to use KWin window rules for legacy system tray icons?](https://forum.kde.org/viewtopic.php?f=111&t=122722)

thinkfan lm_sensors

emacs emacs-goodies

firefox 

libappindicator libappindicator-gtk3 google-chrome-stable google-talkplugin mssttcorefonts

kmenuedit
