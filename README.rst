======================
Personal Fedora Notes
======================

1. `Yum Config`_

2. `Yum Plugins`_

3. `Disable Nouveau`_

4. `Google Chrome`_

5. `RPM Fusion`_

6. `Android`_

7. `Java`_

8. `Thinkfan`_

9. `Media Codecs`_

10. `Bumblebee`_

11. `Moka Icon Theme`_

12. `Dropbox`_

13. `ksuperkey`_

14. `TLP`_

15. `VirtualBox`_

16. `HandBrake`_

17. `Skype`_

18. `RedShift Plasma Widget`_

19. `Dropbox-Dolphin Integration`_

20. `Caffeine`_

21. `Gnome Encfs Manager`_

22. `Genymotion`_

23. `SoundKonverter`_

24. `SSH Key Management`_

25. `reStructuredText`_

26. `Viber`_


Yum Config
----------

- Keep Cache

::

  /etc/yum.conf
  ------------------------
  keepcache=1

Yum Plugins
-----------

::

  sudo yum install yum-plugin-fastestmirror yum-plugin-local \
  yum-plugin-changelog yum-plugin-show-leaves

.. decide which one do you prefer clean_requirements_on_remove=1 or yum-plugin-remove-with-leaves

Disable Nouveau
----------------

- Blacklist ``nouveau`` module

::

  /etc/modprobe.d/blacklist-nouveau.conf
  -------------------------------------------------------
  blacklist nouveau

- Recreate initramfs

::

  sudo mv /boot/initramfs-$(uname -r).img /boot/initramfs-$(uname -r)-nouveau.img
  sudo dracut --omit-drivers nouveau /boot/initramfs-$(uname -r).img $(uname -r)


`Ask Fedora how-to-disable-nouveau-in-fedora-18 <https://ask.fedoraproject.org/en/question/23982/how-to-disable-nouveau-in-fedora-18/>`_

Google Chrome 
-----------------
 
`Chrome <https://www.google.com/intl/en_in/chrome/browser/>`_
 
`Hangouts Plugin <https://www.google.com/tools/dlpage/hangoutplugin>`_

RPM Fusion
------------
 
::

  su -c 'yum localinstall --nogpgcheck http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm
  http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm'


`RPMFusion <http://rpmfusion.org/Configuration>`_

Android
--------

- Install `Java`_


- Android SDK Dependencies

::

  sudo yum install glibc.i686 glibc-devel.i686 libstdc++.i686 zlib-devel.i686 \
  ncurses-devel.i686 libX11-devel.i686 libXrender.i686 libXrandr.i686

- Android Build Dependencies

::

  sudo yum install gcc gcc-c++ gperf flex bison glibc-devel.{x86_64,i686} \
  zlib-devel.{x86_64,i686} ncurses-devel.i686 libsx-devel readline-devel.i686 \
  perl-Switch

- Set Android SDK Path

::
  
  ~/.bashrc
  -----------------------------------------------------
  PATH=$PATH:$HOME/AndroidSDK:$HOME/AndroidSDK/tools
  export PATH

  # For SDK version r_08 and higher, also add this for adb:
  PATH=$PATH:$HOME/AndroidSDK/platform-tools
  export PATH

- ``udev`` rule

::

  cd /etc/udev/rules.d
  wget https://raw.githubusercontent.com/M0Rf30/android-udev-rules/master/51-android.rules
  chmod a+r /etc/udev/rules.d/51-android.rules
  
`Fedora Wiki HOWTO_Setup_Android_Development <https://fedoraproject.org/wiki/HOWTO_Setup_Android_Development>`_

`Using Hardware Devices <http://developer.android.com/tools/device.html>`_

`MORf30 Github <https://github.com/M0Rf30/android-udev-rules/blob/master/51-android.rules>`_


Java
-----

- Install OpenJDK

::

  sudo yum install java-1.7.0-openjdk.x86_64 icedtea-web.x86_64


- Install Oracle Java 6

::

  sudo su
  sh jdk-6u45-linux-x64-rpm.bin
  

- Install Oracle Java 7

::
  
  sudo su
  rpm -ivh jdk-7u60-linux-x64.rpm
  
If upgrading

::
  
  rpm -Uvh jdk-7u60-linux-x64.rpm

- Set Java Path for JDK 6

::

  export JAVA_HOME=/usr/java/jdk1.6.0_45/
  export PATH=$JAVA_HOME/bin:$PATH
  
- Set Java Path for JDK 7

::
  
  export JAVA_HOME=/usr/java/default/
  export PATH=$JAVA_HOME/bin:$PATH
  
- Set Alternatives

::

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


`Oracle Docs <http://docs.oracle.com/javase/7/docs/webnotes/install/linux/linux-jdk.html#install-64-rpm>`_

`if-not-true-then-false.com <http://www.if-not-true-then-false.com/2010/install-sun-oracle-java-jdk-jre-7-on-fedora-centos-red-hat-rhel/>`_

`Fedora Forums <http://forums.fedoraforum.org/showthread.php?t=297016>`_

`John Goltzer Blogspot <http://johnglotzer.blogspot.in/2012/09/alternatives-install-gets-stuck-failed.html>`_


Thinkfan
---------

- Install and enable systemd file

::

  sudo yum install thinkfan
  sudo systemctl enable thinkfan

- Modify config and add output of following command to it prefixing with ``sensors``

::

  find /sys/devices -type f -name "temp*_input"
  
  /etc/thinkfan.conf
  ---------------------------------------------------------------
  sensor /sys/devices/virtual/hwmon/hwmon0/temp1_input
  sensor /sys/devices/platform/coretemp.0/hwmon/hwmon2/temp3_input
  sensor /sys/devices/platform/coretemp.0/hwmon/hwmon2/temp1_input
  sensor /sys/devices/platform/coretemp.0/hwmon/hwmon2/temp2_input
  

Media Codecs
------------

::

  sudo yum install -y amrnb amrwb faac faad2 flac gstreamer1-libav gstreamer1-plugins-bad-freeworld gstreamer1-plugins-ugly \
  gstreamer-ffmpeg gstreamer-plugins-bad-nonfree gstreamer-plugins-espeak gstreamer-plugins-fc gstreamer-plugins-ugly \
  gstreamer-rtsp lame libdca libmad libmatroska x264 xvidcore gstreamer1-plugins-bad-free gstreamer1-plugins-base \
  gstreamer1-plugins-good gstreamer-plugins-bad gstreamer-plugins-bad-free gstreamer-plugins-base gstreamer-plugins-good
  

`Fedy <https://github.com/satya164/fedy/blob/master/plugins/util/media_codecs.sh>`_


Bumblebee
-----------

`Fedora Wiki Bumblebee <https://fedoraproject.org/wiki/Bumblebee>`_


Moka Icon Theme
-------------------

::

  sudo wget http://download.opensuse.org/repositories/home:/snwh:/moka-icon-theme/Fedora_20/home:snwh:moka-icon-theme.repo -O /etc/yum.repos.d/moka-icon-theme.repo
  sudo yum update && sudo yum install moka-icon-theme


`Moka Project <http://mokaproject.com/moka-icon-theme/download/fedora/>`_


Dropbox
--------

::
  
    cd ~ && wget -O - "https://www.dropbox.com/download?plat=lnx.x86_64" | tar xzf -
  ~/.dropbox-dist/dropboxd
  

ksuperkey
----------

- Installation

::
  
  sudo yum install git gcc make libX11-devel libXtst-devel pkgconfig
  git clone https://github.com/hanschen/ksuperkey.git
  cd ksuperkey
  make
  sudo make install
  
- Autostart

::

  ksuperkey -e 'Control_L=Escape;Super_L=Alt_L|F2'

`Github hanschen <https://github.com/hanschen/ksuperkey>`_

TLP
-------

- Configure Repo

::
  
  yum localinstall --nogpgcheck http://repo.linrunner.de/fedora/tlp/repos/releases/tlp-release-1.0-0.noarch.rpm
  yum localinstall --nogpgcheck http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-stable.noarch.rpm

- Installation

::
  
  sudo yum install tlp tlp-rdw akmod-tp_smapi akmod-acpi_call kernel-devel

`Linrunner.de <http://linrunner.de/en/tlp/docs/tlp-linux-advanced-power-management.html#installation Linrunner>`_


VirtualBox
-----------

- Configure Repo

::

  cd /etc/yum.repos.d/
  wget http://download.virtualbox.org/virtualbox/rpm/fedora/virtualbox.repo
  
- Installation

::

  yum install binutils gcc make patch libgomp glibc-headers glibc-devel \
  kernel-headers kernel-devel dkms VirtualBox-4.3
  
- Setup

::

  /etc/init.d/vboxdrv setup
  usermod -a -G vboxusers $USER
  

`Fedoraonline.se <http://www.fedoraonline.se/install-oracle-vm-virtualbox-fedora-20/>`_

`Oracle <https://www.virtualbox.org/wiki/Linux_Downloads>`_


HandBrake 
------------

`Negativo17 HandBrake <http://negativo17.org/handbrake/>`_

Skype
-------

- 32-bit Libraries for 64-bit systems

::

  sudo yum -y install libXv.i686 libXScrnSaver.i686 qt.i686 qt-x11.i686 pulseaudio-libs.i686 \
  pulseaudio-libs-glib2.i686 alsa-plugins-pulseaudio.i686 qtwebkit.i686
  
- Follow Negativo17's post.

`Negativo17 Skype <http://negativo17.org/skype-and-skype-pidgin-plugin/>`_

`Skype.com <https://support.skype.com/en/faq/FA12120/getting-started-with-skype-for-linux>`_

RedShift Plasma Widget
----------------------

::

  sudo yum group install "C Development Tools and Libraries"
  sudo yum install cmake kde-workspace-devel redshift-gtk
  mkdir build
  cd build
  cmake -DCMAKE_INSTALL_PREFIX=$(kde4-config --prefix) ..
  make
  sudo make install


`kde-apps.org <http://kde-apps.org/content/show.php/Redshift+Plasmoid?content=148737>`_


Dropbox-Dolphin Integration
---------------------------

::

  sudo yum install kde-baseapps-devel
  git clone git://anongit.kde.org/scratch/trichard/dolphin-box-plugin
  cd dolphin-box-plugin
  cmake -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_BUILD_TYPE=Release .
  make
  sudo make install


`trichard-kde.blogspot.in <http://trichard-kde.blogspot.in/2010/12/introducing-dropbox-integration-for.html>`_

`aur.archlinux.org <https://aur.archlinux.org/packages/do/dolphin-box-plugin-git/PKGBUILD AUR>`_

Caffeine
---------

`My blog <http://sudhirkhanger.com/2014/03/18/how-to-install-caffeine-in-fedora-20/>`_

`OBS zhonghuaren <http://software.opensuse.org/download.html?project=home%3Azhonghuaren&package=caffeine>`_

Gnome Encfs Manager
--------------------

`libertyzero.com <http://www.libertyzero.com/GEncfsM/>`_

`OBS moritzmolch <http://software.opensuse.org/download.html?project=home:moritzmolch:gencfsm&package=gnome-encfs-manager>`_



Genymotion
------------

::

  ./genymotion-2.2.1_x64.bin
  mkdir /home/donnie/.Genymobile
  touch /home/donnie/.Genymobile/genymotion.log
  rm libQt*


SoundKonverter
--------------

`Github HessiJames <https://github.com/HessiJames/soundkonverter/wiki/Installing-soundKonverter#precompiled_packages>`_

SSH Key Management
---------------------

::

  ssh-keygen -t rsa -f ~/.ssh/github_id_rsa -C "your_email@youremail.com"

  ~/.ssh/config
  --------------------------------------------
  Host github
  User git
  Hostname github.com
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/github_id_rsa

- Change config file permission

::

  chmod 600 ~/.ssh/config
  
  ssh-add ~/.ssh/github_id_rsa

Add ssh password in ksshaskpass by running following command in KRunner

::
  
  ssh-add ~/.ssh/github_id_rsa`

Add the same like to autostart also to make key get unlocked automatically

https://help.github.com/articles/generating-ssh-keys

http://dbushell.com/2013/01/27/multiple-accounts-and-ssh-keys/

http://www.robotgoblin.co.uk/blog/2012/07/24/managing-multiple-ssh-keys/

http://wiki.gentoo.org/wiki/Keychain

Viber
------
::

   ar p viber.deb data.tar.gz | tar zx

`Ask Fedora viber-on-fedora <https://ask.fedoraproject.org/en/question/45112/viber-on-fedora/>`_
`Viber.com <http://www.viber.com/>`_

reStructuredText
-----------------

::

  sudo yum install python-docutils python-sphinx
