1. Display
   1. `Nvidia X Server Settings` > `X Server Display Configuration` > Specify display order and set resolutions
   1. Check `Display Configuration > Scale` and `Fonts > Font dpi`
   1. Restart
   1. Right Click on Panel > `Edit Panel...` > Change Height
1. Keyboard Layouts
   1. `Keyboard > Layouts > Add`
   2. `Keyboard > Layouts > Layout Indicator: Show flag`
1. fstab
   1. *prerequizites*: /home already mounted to separate partition
   2. copy user's content and /var to new place:
   ```bash
   sudo mkdir /home/home && sudo mkdir /home/var
   sudo cp -a /home/gorshkov /home/home
   sudo cp -a /home/lost+found /home/home
   sudo cp -a /var/* /home/home/var
   ```
   3. remount `home` and `var` folders
      1. Comment folder that looks like: `UUID=c1d735cd-4aac-4725-bb11-265df8adc544 /home                ext4    defaults        0       2`
      2. Add partition as root with the same UUID as above and then mount specific folder with `rbind` option:
      ```bash
      sudo mkdir -p /mnt/hdd/sdb2
      ```
      ```bash
       # /home was on /dev/sdb2 during installation
       UUID=c1d735cd-4aac-4725-bb11-265df8adc544  /mnt/hdd/sdb2        ext4    defaults        0       2
       /mnt/hdd/sdb2/var                          /var                 none    rbind           0       0
       /mnt/hdd/sdb2/home                         /home                none    rbind           0       0
      ```
      3. You could mount any partitions even `ntfs` (as below), UUID can be obtained via `KDE Partittion Manager`:
      ```bash
      sudo mkdir -p /mnt/ssd/nvme0n1p1
      sudo mkdir -p /mnt/ssd/nvme1n1p3
      sudo mkdir -p /mnt/hdd/sdb1
      ```
      ```bash
      # windows (samsung 950)
      UUID=C4F0C3D5F0C3CC3C                      /mnt/ssd/nvme0n1p1   ntfs    ro              0       2

      # windows (samsung 970)
      UUID=01D631CAEA750260                      /mnt/ssd/nvme1n1p3   ntfs    ro              0       2

      # ntfs data (wd)
      UUID=01D631C6910C33F0                      /mnt/hdd/sdb1        ntfs    defaults        0       2
      ```
   4. Delete old folders 
   ```bash
   sudo rm -r /mnt/hdd/sdb2/gorshkov
   sudo rm -r /mnt/hdd/sdb2/lost+found
   ```
1. VPN 
   1. Cisco AnyConnect 
1. Applications   
   1. [Google Chrome](https://www.google.com/intl/ru_ru/chrome/). Download `DEB` package and start installation
   1. qBittorrent: `sudo apt install qbittorrent`
   1. git: `sudo apt install git`
   1. [IntellijIdea(see 2020.1.1)](https://www.jetbrains.com/ru-ru/idea/download/#section=linux), [treatment](https://rutracker.org/forum/viewtopic.php?t=5883972)
   1. [Zoom](https://zoom.us/download)
   1. Remote Desktops:
      1. `sudo apt-get install remmina remmina-plugin-*`
      1. https://coderwall.com/p/b982hw/linux-remote-desktop-multiple-monitor-support
      1. https://medium.com/analytics-vidhya/linux-remote-desktop-multiple-monitor-support-840974e9eb73
   1. Open JDK
      1. `sudo apt install default-jre`
      1. `sudo apt install openjdk-11-jre-headless`
   1. [Oracle JDK](https://www.oracle.com/java). 
      1. [Download](https://www.oracle.com/java/technologies/javase-downloads.html) `Debian Package` and install it.
      2. `sudo update-alternatives --install /usr/bin/java /usr/lib/jvm/jdk-11.0.7/bin/java 120`
      3. `sudo update-alternatives --install /usr/bin/javac /usr/lib/jvm/jdk-11.0.7/bin/javac 120`
      4. `sudo update-alternatives --install /usr/bin/keytool /usr/lib/jvm/jdk-11.0.7/bin/keytool 120`
      5. `sudo update-alternatives --install /usr/bin/jarsigner /usr/lib/jvm/jdk-11.0.7/bin/jarsigner 120`      
      6. check `sudo update-alternatives --config java`
      100. + [How to INSTALL TO SERVER](https://www.digitalocean.com/community/tutorials/how-to-install-java-with-apt-on-ubuntu-20-04-ru):
   1. [Maven](http://maven.apache.org). [How to install](https://www.apache-maven.ru/install.html): 
      1. Download http://maven.apache.org/download.html
      2. `sudo mkdir -p /opt/maven && sudo cp /home/gorshkov/Downloads/apache-maven-3.6.3-bin.tar.gz /opt/maven`
      3. `sudo tar -xvf /opt/maven/apache-maven-3.6.3-bin.tar.gz`
      4. `sudo sh -c 'echo "export M2_HOME=/opt/maven/apache-maven-3.6.3" >> /etc/profile' && source /etc/profile`
         **OR**
         `echo "export M2_HOME=/opt/maven/apache-maven-3.6.3" >> ~/.profile && source ~/.profile`
      5. `sudo update-alternatives --install /usr/bin/mvn mvn "${M2_HOME}/bin/mvn" 120`
      6. restart
   
Useful Links:
* [13 Keyboard Shortcut Every Ubuntu 18.04 User Should Know](https://itsfoss.com/ubuntu-shortcuts/)
