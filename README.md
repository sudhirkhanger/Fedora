# Personal Fedora Notes

* [Java](#java)
 * [Oracle JDK 8](#oracle-java-8)

## Remove

    sudo dnf remove kmahjongg kmines kpat kolourpaint konqueror krusader liveusb-creator amarok-libs \
    calligra-libs qupzilla krdc krfb kruler kcolorchooser dnfdragora konqueror
    
## Install

    sudo dnf install gnome-icon-theme breeze-gtk

## Java

### Open JDK 8

    sudo dnf install java-1.8.0-openjdk.x86_64 java-1.8.0-openjdk-devel.x86_64 java-1.8.0-openjdk-demo.x86_64 \
    java-1.8.0-openjdk-javadoc.noarch icedtea-web

### Oracle Java 8

#### Install

	sudo su
	rpm -ivh jdk-8u25-linux-x64.rpm

#### Upgrade

	rpm -Uvh jdk-8u25-linux-x64.rpm
	
#### Using Dnf

    sudo dnf install jdk-8u112-linux-x64.rpm
	
#### Setup environmental variables

	emacs -nw .bashrc
	
	export JAVA_HOME=/usr/java/default/
	export PATH=$JAVA_HOME/bin:$PATH

Source: [1](https://docs.oracle.com/javase/8/docs/technotes/guides/install/linux_jdk.html#BJFJHFDD)

### Android

#### Latest Android Studio dependencies

    sudo dnf install zlib.i686 ncurses-libs.i686 bzip2-libs.i686 libgcc.i686

#### udev Rules

	cd /etc/udev/rules.d
	wget https://raw.githubusercontent.com/M0Rf30/android-udev-rules/master/51-android.rules
	chmod a+r /etc/udev/rules.d/51-android.rules

#### Virtualization (Only one)

    sudo dnf install qemu-kvm libvirt

### Genymotion

	./genymotion-2.2.1_x64.bin
	
#### Android SDK Environmental Variable

	~/.bashrc
	export ANDROID_HOME=/home/sudhir/Documents/Android/sdk
	export PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools

Source: [1](https://developer.android.com/studio/troubleshoot.html#linux-libraries) [2](https://github.com/M0Rf30/android-udev-rules/blob/master/51-android.rules)

### TLP

#### Configure Repo

	sudo dnf install http://repo.linrunner.de/fedora/tlp/repos/releases/tlp-release-1.0-0.noarch.rpm
	sudo dnf install http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-stable.noarch.rpm

#### Installation

	sudo dnf install tlp tlp-rdw akmod-tp_smapi akmod-acpi_call kernel-devel

[Linrunner.de](http://linrunner.de/en/tlp/docs/tlp-linux-advanced-power-management.html#installation)

### Speed up LibreOffice

    sudo dnf group install LibreOffice

- Undo steps 20 or 30 steps
- Under Graphics cache, set Use for LibreOffice to 128 MB
- Set Memory per object to 20 MB (up from the default 5 MB).

### Google Chrome

	sudo dnf install google-chrome-stable    
	sudo rpm --import https://dl-ssl.google.com/linux/linux_signing_key.pub

## Graphics

### Gimp

    sudo dnf install gimp.x86_64 gmic-gimp.x86_64 gimp-help.noarch gimp-resynthesizer.x86_64

### Design

    sudo dnf install inkscape.x86_64 pencil

## Developmental

    sudo dnf install git cmake tmux sqlitebrowser
    sudo dnf group install "C Development Tools and Libraries"

## Disable MCE Check

    /etc/abrt/plugins/oops.conf
    OnlyFatalMCE = yes

## VirtualBox

### RPMFusion

    sudo dnf install VirtualBox kernel-devel-$(uname -r) akmod-VirtualBox

#### Generate VirtualBox modules

    sudo akmods --force
    systemctl restart systemd-modules-load.service
    
[Source](https://rpmfusion.org/Howto/VirtualBox)

#### Rebuild

    sudo akmods --force
    sudo dracut -v -f
    sudo grub2-mkconfig -o /boot/efi/EFI/fedora/grub.cfg
    
### Oracle's VirtualBox

#### Setup Repo

	su -
	cd /etc/yum.repos.d/
	wget http://download.virtualbox.org/virtualbox/rpm/fedora/virtualbox.repo

#### Add key (if not installed on its own)

    wget https://www.virtualbox.org/download/oracle_vbox.asc
    sudo rpm --import oracle_vbox.asc

#### Installation

	dnf install binutils gcc make patch libgomp glibc-headers glibc-devel kernel-headers kernel-devel dkms
	sudo dnf install VirtualBox-5.2.x86_64
	
#### Rebuild Module

	sudo /usr/lib/virtualbox/vboxdrv.sh setup
	
### VirtualBox Guest Additions

    sudo dnf -y install gcc automake make kernel-headers kernel-devel perl
    sudo /run/media/user/VBOXADDITIONS*/VBoxLinuxAdditions.run
    
[Source](http://www.if-not-true-then-false.com/2010/install-virtualbox-with-yum-on-fedora-centos-red-hat-rhel/)

### Common Add User

    sudo usermod -a -G vboxusers $USER

## Multimedia

### Players

    sudo dnf install vlc juk
    
### Media Codecs

    sudo dnf install amrnb amrwb faac faad2 flac gstreamer1-libav gstreamer1-plugins-bad-freeworld gstreamer1-plugins-ugly \
    gstreamer-ffmpeg gstreamer-plugins-bad-nonfree gstreamer-plugins-espeak gstreamer-plugins-fc gstreamer-plugins-ugly \
    gstreamer-rtsp lame libdca libmad libmatroska x264 xvidcore gstreamer1-plugins-bad-free gstreamer1-plugins-base \
    gstreamer1-plugins-good gstreamer-plugins-bad gstreamer-plugins-bad-free gstreamer-plugins-base gstreamer-plugins-good

### VA-API

    sudo dnf install libva.x86_64 libva-utils.x86_64 libva-intel-driver.x86_64 libva-intel-hybrid-driver

#### Check Status

	vainfo

### VDPAU

    sudo dnf install vdpauinfo libva-vdpau-driver libvdpau-va-gl libva-utils

#### Config

    emacs -nw ~/.bashrc
    # VDAPU Support
    export VDPAU_DRIVER=va_gl

#### Check Status

	vdpauinfo

---

### Alternative Codecs from UnitedRPMs

#### UnitedRPMs

    su -c 'dnf -y install https://raw.githubusercontent.com/UnitedRPMs/unitedrpms/master/RPM/unitedrpms-24-2.noarch.rpm'
    su -c 'rpm --import https://raw.githubusercontent.com/UnitedRPMs/unitedrpms.github.io/master/URPMS-GPG-PUBLICKEY-Fedora-24'

#### GNOME with gstreamer
    
	sudo dnf install gstreamer{1,}-{ffmpeg,libav,plugins-{good,ugly,bad{,-free,-nonfree}}} --setopt=strict=0
    
#### Plasma with gstreamer

    sudo dnf install gstreamer{1,}-{ffmpeg,libav,plugins-{good,ugly,bad{,-free,-nonfree}}} --setopt=strict=0

#### Plasma with Phonon
    
	sudo dnf install phonon-qt5-backend-gstreamer phonon-backend-gstreamer

[The Linux Home Front Project](https://tlhp.cf/unitedrpms-rpmfusion-alternative/)

---

## Apps

    sudo dnf install keepassxc emacs

## Utilities

    sudo dnf install youtube-dl htop powertop python3-dnf-plugin-tracer.noarch pandoc \
    nmap ImageMagick lm_sensors unrar simple-mtpfs

## KDE Apps

    sudo dnf install digikam soundkonverter
	
## KDE Utilities

    sudo dnf install k3b-extras-freeworld akonadiconsole kdesdk-thumbnailers ffmpegthumbs unar kio_mtp

## Fonts

    sudo dnf install levien-inconsolata-fonts adobe-source-code-pro-fonts.noarch \
    adobe-source-sans-pro-fonts.noarch open-sans-fonts.noarch google-noto-emoji-fonts google-noto-sans-old-turkic-fonts

### Microsoft Core Fonts

    sudo yum install msttcore-fonts-installer-2.6-1.noarch.rpm
    
[mscorefonts2 Sourceforge](http://sourceforge.net/projects/mscorefonts2/?source=typ_redirect)

### Qt Online Installer

    sudo dnf group install "C Development Tools and Libraries"
    sudo dnf install mesa-libGL-devel

[Source](https://doc.qt.io/qt-5/linux.html)

### Suspend to Disk

    sudo nano /etc/default/grub
    sudo blkid
    GRUB_CMDLINE_LINUX="resume=UUID="swap-partition-uuid"
    sudo grub2-mkconfig -o /boot/efi/EFI/fedora/grub.cfg

## Nodejs

### Installation

    sudo dnf install nodejs npm

### Setup local npm installation

The following guide has been taken from sindresorhus's GitHub [page](https://github.com/sindresorhus/guides/blob/master/npm-global-without-sudo.md).

    * Create npm package folder
    mkdir "${HOME}/.npm-packages"

    * Add location to `~/.npmrc` file.
    prefix=${HOME}/.npm-packages

    * Add config to `~/.bashrc` file
    NPM_PACKAGES="${HOME}/.npm-packages"

    PATH="$NPM_PACKAGES/bin:$PATH"

    # Unset manpath so we can inherit from /etc/manpath via the `manpath` command
    unset MANPATH # delete if you already modified MANPATH elsewhere in your config
    export MANPATH="$NPM_PACKAGES/share/man:$(manpath)"


### Screencasting
    
    sudo dnf install key-mon simplescreenrecorder.x86_64 ffmpeg
    
## Video Editing

    sudo dnf install kdenlive frei0r-plugins obs-studio
	
## GTK+ White on white bug

    nano ~/.gtkrc-2.0-kde4
    
    style "gnome-color-chooser-tooltips"
    {
    bg[NORMAL] = "#FFFFAF"
    fg[NORMAL] = "#000000"
    }
    widget "gtk-tooltip*" style "gnome-color-chooser-tooltips"

## Write disk using ddrescue

    sudo dnf install ddrescue
    sudo ddrescue -D --force kubuntu-16.04.1-desktop-amd64.iso /dev/sdb

## Disable Horizontal Scrolling

    /etc/X11/xorg.conf.d/30-touchpad.conf
    Section "InputClass"
        Identifier "Disable Horizontal Scrolling"
        MatchIsTouchpad "on"
        MatchDriver "libinput"
        Option "HorizontalScrolling" "false"
	EndSection

## SDKMAN

    export SDKMAN_DIR="/home/sudhir/.local/bin/sdkman" && curl -s "https://get.sdkman.io" | bash
	sdk install gradle

## Lock a package version

	sudo dnf install python3-dnf-plugin-versionlock
	dnf versionlock add package-name

## Write ISO to the usb

	sudo dd bs=4M if=Fedora-KDE-Live-x86_64-28-1.1.iso of=/dev/sda status=progress oflag=direct
	
---

* ~/.bashrc
* .ssh
* npm
* .emacs.d
* .face.icon
* .gitconfig
* bash history
* xresources
* darcula theme - konsole, emacs, possibly kwrite
* ~/.local/scripts
* ~/.gradle/gradle.properties
* libinput horizontal scroll
* sdkmann
