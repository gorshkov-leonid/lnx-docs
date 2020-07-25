1. Display
   1. `Nvidia X Server Settings` > `X Server Display Configuration` > Specify display order and set resolutions
   1. Check `Display Configuration > Scale` and `Fonts > Font dpi`
   1. Restart
   1. Right Click on Panel > `Edit Panel...` > Change Height
1. Keyboard Layouts
   1. `Keyboard > Layouts > Add`
   2. `Keyboard > Layouts > Layout Indicator: Show flag`
1. Make the same as in Windows 
   ```
   sudo timedatectl set-local-rtc 1
   ```
1. enable `su` for root
   ```
   sudo passwd root
   ```
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
   1. `sudo apt install curl`
   1. `sudo apt install nano`
   1. `sudo apt install mc`
   1. `sudo apt install git`
   1. `sudo apt install net-tools` (ifconfig)
   1. [Google Chrome](https://www.google.com/intl/ru_ru/chrome/). Download `DEB` package and start installation
   1. qBittorrent: `sudo apt install qbittorrent`
   1. [IntellijIdea(see 2020.1.1)](https://www.jetbrains.com/ru-ru/idea/download/#section=linux), [treatment](https://rutracker.org/forum/viewtopic.php?t=5883972)
   1. [Zoom](https://zoom.us/download)
   1. Remote Desktops:
      1. `sudo apt-get install remmina remmina-plugin-*`
      1. https://coderwall.com/p/b982hw/linux-remote-desktop-multiple-monitor-support
      1. https://medium.com/analytics-vidhya/linux-remote-desktop-multiple-monitor-support-840974e9eb73
   1. Open JDK
      1. `sudo apt install default-jre`
      1. `sudo apt install openjdk-11-jre-headless`
   1. [Oracle JDK](https://www.oracle.com/java). See [article](https://www.digitalocean.com/community/tutorials/how-to-install-java-with-apt-on-ubuntu-20-04-ru).
      1. [Download](https://www.oracle.com/java/technologies/javase-downloads.html) `Debian Package` and install it.
      2. `sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk-11.0.7/bin/java 2000`
      3. `sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk-11.0.7/bin/javac 2000`
      4. `sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk-11.0.7/bin/javap 2000`
      5. `sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk-11.0.7/bin/jar 2000`
      6. `sudo update-alternatives --install /usr/bin/keytool keytool /usr/lib/jvm/jdk-11.0.7/bin/keytool 2000`
      7. `sudo update-alternatives --install /usr/bin/jarsigner jarsigner /usr/lib/jvm/jdk-11.0.7/bin/jarsigner 2000`      
      8. `sudo update-alternatives --install /usr/bin/keytool keytool /usr/lib/jvm/jdk-11.0.7/bin/jstat 2000`
      9. `sudo update-alternatives --install /usr/bin/keytool keytool /usr/lib/jvm/jdk-11.0.7/bin/jmap 2000`
      10. `sudo update-alternatives --install /usr/bin/keytool keytool /usr/lib/jvm/jdk-11.0.7/bin/jstack 2000`
      11. `sudo update-alternatives --install /usr/bin/jarsigner jarsigner /usr/lib/jvm/jdk-11.0.7/bin/jfr 2000`      
      12. `sudo update-alternatives --install /usr/bin/jarsigner jarsigner /usr/lib/jvm/jdk-11.0.7/bin/jjs 2000`      
      13. check `sudo update-alternatives --config java`      
      14. sudo sh -c 'echo "export JAVA_HOME=/usr/lib/jvm/jdk-11.0.7" >> /etc/profile' && source /etc/profile 
          **OR**
          `echo "export JAVA2_HOME=/usr/lib/jvm/jdk-11.0.7" >> ~/.profile && source ~/.profile`
      16. restart    
      
   1. [Maven](http://maven.apache.org). [How to install](https://www.apache-maven.ru/install.html): 
      1. Download http://maven.apache.org/download.html
      2. `sudo mkdir -p /opt/maven && sudo cp /home/gorshkov/Downloads/apache-maven-3.6.3-bin.tar.gz /opt/maven`
      3. `sudo tar -xvf /opt/maven/apache-maven-3.6.3-bin.tar.gz`
      4. `sudo update-alternatives --install /usr/bin/mvn mvn "${M2_HOME}/bin/mvn" 120`
      5. check `sudo update-alternatives --config mvn`
      6. `sudo sh -c 'echo "export M2_HOME=/opt/maven/apache-maven-3.6.3" >> /etc/profile' && source /etc/profile`
         **OR**
         `echo "export M2_HOME=/opt/maven/apache-maven-3.6.3" >> ~/.profile && source ~/.profile`
      7. restart
   1. node/npm
      1. [Установить node через пакетный менеджер](https://nodejs.org/ru/download/package-manager/). Выбрать nvm.
      2. `nvm install 10.13.0`
      3. `npm set editor mcedit`
      3. `npm config set @mycorp:registry "<corp-registry-url>"`
   1. [docker](https://docker.com)
      1. [Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/). To be better use repositories.
      2. [post-install](https://docs.docker.com/engine/install/linux-postinstall/#manage-docker-as-a-non-root-user)
      To have ability of run without sudo run this script and then relogin:
      ```
      sudo groupadd docker
      sudo usermod -aG docker $USER
    
      ```
      3. Support VPN
         1. Make sure that `jq` installed
         ```
         sudo apt  install jq
         ```
         2. Prepare script that can be run every time when VPN turned on/off
         ```
         mkdir -p "$(systemd-path user-binaries)"
         export DOCKER_CONF_SH="$(systemd-path user-binaries)/docker-conf.sh"

         cat > $DOCKER_CONF_SH << "EOF"

         if [[ ! -f /etc/docker/daemon.json ]]; then echo '{ "bip": "172.18.1.1/24", "fixed-cidr": "172.18.1.1/24" }' | sudo tee /etc/docker/daemon.json > /dev/null; fi

         export RESOLVE_CONF="$(cat /etc/resolv.conf)"
         export DAEMON_JSON="$(cat /etc/docker/daemon.json)" 

         export DNS_JSON="[$( echo "$RESOLVE_CONF" | grep nameserver | cut -d" " -f2 | sed -e 's/.*/"&"/; /127\.0\.0\.53/d' | paste -sd "," - | awk '{print $1",\"8.8.8.8\",\"8.8.4.4\""}' )]" 
         export DAEMON_JSON="$(echo "$DAEMON_JSON" | awk '{if (!$1) print "{}"; else print $0;}' | jq '.dns = '$DNS_JSON)"

         export DOMAIN_JSON="[$( echo "$RESOLVE_CONF" | grep search | cut -d" " -f2 | sed 's/.*/"&"/' | paste -sd "," - )]" 
         export DAEMON_JSON="$(echo "$DAEMON_JSON" | awk '{if (!$1) print "{}"; else print $0;}' | jq '.["dns-search"] = '$DOMAIN_JSON)"

         echo "$DAEMON_JSON" | sudo tee /etc/docker/daemon.json > /dev/null

         EOF

         chmod 740 $DOCKER_CONF_SH
         ```
         3. Run `docker-conf.sh && systemctl restart docker.service` to apply VPN changes
      4. To make docker to be run on host run this script and then reopen terminal:    
         ```
         cat | sudo tee -a ~/.bashrc /root/.bashrc > /dev/null << "EOF"

         function docker() {
             if [ "$1" == "run" ]; then
                 bash -c 'command docker run --network host '"${@:2}"
             elif [ "$1" == "build" ]; then
                 bash -c 'command docker build --network host '"${@:2}"
             else
                 command docker "$@"
             fi
         }
         export -f docker
         
         EOF         
         ```
   1. minikube
      1. [install-kubctl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
      1. [install-minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/)
      1. [Minikube + KVM/Installation](https://minikube.sigs.k8s.io/docs/drivers/kvm2/), [KVM(debian)](https://wiki.debian.org/KVM#Installation)
         ```
         sudo apt-get install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils
         sudo apt-get install virt-manager
         ```
         * --driver=none(host) / docker / podman(docker under root) / kvm2    
         *  --kvm-gpu=true
      
   
Useful Links:
* [13 Keyboard Shortcut Every Ubuntu 18.04 User Should Know](https://itsfoss.com/ubuntu-shortcuts/)
