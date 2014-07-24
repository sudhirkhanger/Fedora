=========================
Personal Fedora Notes
=========================

* [SSH Key](#sshkey)

Yum Config
----------
::
  emacs -nw /etc/yum.conf
  keepcache=1
  metadata_expire=1d

Yum Plugins
-----------
::
  sudo yum install yum-plugin-fastestmirror yum-plugin-local yum-plugin-changelog yum-plugin-show-leaves

Disable Nouveau
----------------
::
  emacs -nw /etc/modprobe.d/blacklist-nouveau.conf
  blacklist nouveau

::
  sudo mv /boot/initramfs-$(uname -r).img /boot/initramfs-$(uname -r)-nouveau.img
  sudo dracut --omit-drivers nouveau /boot/initramfs-$(uname -r).img $(uname -r)


Ask Fedora https://ask.fedoraproject.org/en/question/23982/how-to-disable-nouveau-in-fedora-18/

== Google Chrome ==
[https://www.google.com/intl/en_in/chrome/browser/ Google Chrome]

[https://www.google.com/tools/dlpage/hangoutplugin Google Talk Plugin]

== RPM Fusion ==
<pre>
su -c 'yum localinstall --nogpgcheck http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm 

http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm'</pre>

[http://rpmfusion.org/Configuration RPM Fusion]

Android
--------

- Install Java
::
  sudo yum install java-1.7.0-openjdk.x86_64 icedtea-web.x86_64

::
  su -
  sh jdk-6u45-linux-x64-rpm.bin

::
  export JAVA_HOME=/usr/java/jdk1.6.0_45/
  export PATH=$JAVA_HOME/bin:$PATH

Android SDK Dependencies
<pre>
sudo yum install glibc.i686 glibc-devel.i686 libstdc++.i686 zlib-devel.i686 ncurses-devel.i686 libX11-devel.i686
libXrender.i686 libXrandr.i686
</pre>

Android Build Dependencies
<pre>
sudo yum install gcc gcc-c++ gperf flex bison glibc-devel.{x86_64,i686} zlib-devel.{x86_64,i686} ncurses-devel.i686 libsx-devel
readline-devel.i686 perl-Switch
</pre>

<pre>
PATH=$PATH:$HOME/AndroidSDK:$HOME/AndroidSDK/tools
export PATH

# For SDK version r_08 and higher, also add this for adb:
PATH=$PATH:$HOME/AndroidSDK/platform-tools
export PATH
</pre>

<pre>
sudo touch /etc/udev/rules.d/51-android.rules
sudo nano /etc/udev/rules.d/51-android.rules
sudo chmod a+r /etc/udev/rules.d/51-android.rules
</pre>

[https://fedoraproject.org/wiki/HOWTO_Setup_Android_Development Fedora Wiki]

[https://developer.android.com/tools/device.html#setting-up Android Hardware]

[https://github.com/M0Rf30/android-udev-rules/blob/master/51-android.rules android-udev]

== Thinkfan ==
<pre>
sudo yum install thinkfan
sudo systemctl enable thinkfan

nano /etc/thinkfan.conf

find /sys/devices -type f -name "temp*_input"

sensor /sys/devices/virtual/hwmon/hwmon0/temp1_input
sensor /sys/devices/platform/coretemp.0/temp3_input
sensor /sys/devices/platform/coretemp.0/temp1_input
sensor /sys/devices/platform/coretemp.0/temp2_input

</pre>

== Media Codes ==
<pre> 
sudo yum install -y amrnb amrwb faac faad2 flac gstreamer1-libav gstreamer1-plugins-bad-freeworld gstreamer1-plugins-ugly \
gstreamer-ffmpeg gstreamer-plugins-bad-nonfree gstreamer-plugins-espeak gstreamer-plugins-fc gstreamer-plugins-ugly \
gstreamer-rtsp lame libdca libmad libmatroska x264 xvidcore gstreamer1-plugins-bad-free gstreamer1-plugins-base \
gstreamer1-plugins-good gstreamer-plugins-bad gstreamer-plugins-bad-free gstreamer-plugins-base gstreamer-plugins-good
</pre>

[https://github.com/satya164/fedy/blob/master/plugins/util/media_codecs.sh Fedy]

== Bumblebee ==

[https://fedoraproject.org/wiki/Bumblebee Fedora Wiki]

== Moka Icon Theme ==

<pre>
sudo wget http://download.opensuse.org/repositories/home:/snwh:/moka-icon-theme/Fedora_20/home:snwh:moka-icon-theme.repo -O /etc/yum.repos.d/moka-icon-theme.repo
sudo yum update
sudo yum install moka-icon-theme
</pre>

[http://mokaproject.com/moka-icon-theme/download/fedora/ Moka Project]

== Dropbox ==
<pre>
cd ~ && wget -O - "https://www.dropbox.com/download?plat=lnx.x86_64" | tar xzf -
~/.dropbox-dist/dropboxd
</pre>

== ksuperkey ==
 https://github.com/hanschen/ksuperkey
<pre>
sudo yum install git gcc make libX11-devel libXtst-devel pkgconfig
git clone https://github.com/hanschen/ksuperkey.git
cd ksuperkey
make
sudo make install
ksuperkey -e 'Control_L=Escape;Super_L=Alt_L|F2'
</pre>

== tlp ==
<pre>
yum localinstall --nogpgcheck http://repo.linrunner.de/fedora/tlp/repos/releases/tlp-release-1.0-0.noarch.rpm
yum localinstall --nogpgcheck http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-stable.noarch.rpm

sudo yum install tlp tlp-rdw akmod-tp_smapi akmod-acpi_call kernel-devel</pre>

[http://linrunner.de/en/tlp/docs/tlp-linux-advanced-power-management.html#installation Linrunner]

== VirtualBox ==
[http://www.fedoraonline.se/install-oracle-vm-virtualbox-fedora-20/ Oracle]

== HandBrake ==
[http://negativo17.org/handbrake/ Negativo17]

== Skype ==
<pre>
sudo yum -y install libXv.i686 libXScrnSaver.i686 qt.i686 qt-x11.i686 pulseaudio-libs.i686 \
pulseaudio-libs-glib2.i686 alsa-plugins-pulseaudio.i686 qtwebkit.i686
</pre>

[http://negativo17.org/skype-and-skype-pidgin-plugin/ Negativo17]

[https://support.skype.com/en/faq/FA12120/getting-started-with-skype-for-linux Skype.com]

== RedShift KDE Widget ==
<pre>
sudo yum group install "C Development Tools and Libraries"
sudo yum install cmake kde-workspace-devel redshift-gtk
mkdir build
cd build
cmake -DCMAKE_INSTALL_PREFIX=$(kde4-config --prefix) ..
make
sudo make install
</pre>

[http://kde-apps.org/content/show.php/Redshift+Plasmoid?content=148737 kde-apps.org]

== Dropbox Dolphin Integration ==
<pre>
sudo yum install kde-baseapps-devel
git clone git://anongit.kde.org/scratch/trichard/dolphin-box-plugin
cd dolphin-box-plugin
cmake -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_BUILD_TYPE=Release .
make
sudo make install
</pre>

[http://trichard-kde.blogspot.in/2010/12/introducing-dropbox-integration-for.html trichard-kde.blogspot.in]

[https://aur.archlinux.org/packages/do/dolphin-box-plugin-git/PKGBUILD AUR]

== Caffeine == 
[http://sudhirkhanger.com/2014/03/18/how-to-install-caffeine-in-fedora-20/ My Blog]

[http://software.opensuse.org/download.html?project=home%3Azhonghuaren&package=caffeine OBS]

== Gnome Encfs Manager ==

[http://www.libertyzero.com/GEncfsM/ libertyzero.com]

[http://software.opensuse.org/download.html?project=home:moritzmolch:gencfsm&package=gnome-encfs-manager OBS]

== Java ==
<pre>
rpm -Uvh jdk-7u<version>-linux-x64.rpm

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

export JAVA_HOME=/usr/java/default/
export PATH=$JAVA_HOME/bin:$PATH
</pre>

[http://docs.oracle.com/javase/7/docs/webnotes/install/linux/linux-jdk.html#install-64-rpm Oracle Docs]

[http://www.if-not-true-then-false.com/2010/install-sun-oracle-java-jdk-jre-7-on-fedora-centos-red-hat-rhel/ if-not-true-then-false.com]

[http://forums.fedoraforum.org/showthread.php?t=297016 FedoraForums]

[http://johnglotzer.blogspot.in/2012/09/alternatives-install-gets-stuck-failed.html johngoltzer]

== Genymotion ==
<pre>
./genymotion-2.2.1_x64.bin
mkdir /home/donnie/.Genymobile
touch /home/donnie/.Genymobile/genymotion.log
rm libQt*
</pre>

== SoundKonverter ==
https://github.com/HessiJames/soundkonverter/wiki/Installing-soundKonverter#precompiled_packages

#### SSH Key Management<a name="sshkey"></a>

```
ssh-keygen -t rsa -f ~/.ssh/github_id_rsa -C "your_email@youremail.com"
```
```
emacs -nw ~/.ssh/config
--------------------------------------------
      Host github
      User git
      Hostname github.com
      PreferredAuthentications publickey
      IdentityFile ~/.ssh/github_id_rsa
```

Change config file permission

`chmod 600 ~/.ssh/config`

```
ssh-add ~/.ssh/github_id_rsa
```
Add ssh password in ksshaskpass by running following command in KRunner

`ssh-add ~/.ssh/github_id_rsa`

Add the same like to autostart also to make key get unlocked automatically

https://help.github.com/articles/generating-ssh-keys

http://dbushell.com/2013/01/27/multiple-accounts-and-ssh-keys/

http://www.robotgoblin.co.uk/blog/2012/07/24/managing-multiple-ssh-keys/

http://wiki.gentoo.org/wiki/Keychain

Viber
=======
::

   ar p viber.deb data.tar.gz | tar zx

`Ask Fedora <https://ask.fedoraproject.org/en/question/45112/viber-on-fedora/>`_
`Viber.com <http://www.viber.com/>`_
