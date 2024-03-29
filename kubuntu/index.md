1. Display
   1. `Nvidia X Server Settings` > `X Server Display Configuration` > Specify display order and set resolutions
   1. Check `Display Configuration > Scale` and `Fonts > Font dpi`
   1. Restart
   1. Right Click on Panel > `Edit Panel...` > Change Height
1. Keyboard Layouts
   1. `Keyboard > Layouts > Add`
   2. `Keyboard > Layouts > Layout Indicator: Show flag`
1. Configure panle on second desktop
   1. Click on the desktop -> Add Panel -> Application Menu Bar / Default Panel
1. Make time the same as in Windows 
   ```
   sudo timedatectl set-local-rtc 1
   ```
1. enable `su` for root(bad practice)
   ```
   sudo passwd root
   ```
   to remove call:
   ```
   sudo passwd -d root
   ```
1. [Boot order](https://help.ubuntu.ru/wiki/grub)
   1. Find necessary menu enrty `cat /boot/grub/grub.cfg | grep menuentry`. E. g. `menuentry 'Windows Boot Manager .... $menuentry_id_option 'osprober-efi-568C-FEE0'`
   1. Set `GRUB_DEFAULT` in `/etc/default/grub` to chosen entry's id
   1. Call `sudo update-grub`
1. fstab
   1. *prerequizites*: /home already mounted to separate partition
   2. copy user's content and /var to new place:
   ```bash
   sudo mkdir /home/home && sudo mkdir /home/var
   sudo cp -a /home/$USER /home/home
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
   sudo rm -r /mnt/hdd/sdb2/$USER
   sudo rm -r /mnt/hdd/sdb2/lost+found
   ```
1. VPN 
   1. Cisco AnyConnect 
   1. If CiscoAnyConnect disconnected then use script and restart gui client
      ```
      sudo service vpnagentd restart 
      sudo service systemd-resolved restart
      sudo service NetworkManager restart      
      ```
1. Applications   
   1. `sudo apt install curl`
   1. `sudo apt install nano`
   1. `sudo apt install mc`
   1. `sudo apt install git`
   1. `sudo apt install net-tools` (ifconfig)
   1. [xclip as pbcopy](https://garywoodfine.com/use-pbcopy-on-ubuntu/)
   1. graphic editors
      1. `sudo apt-get install pinta`
      2. krita
   1. Hardware info
      1. `sudo apt-get install hardinfo`
      1. `sudo apt-get install cpu-x`
      1. `sudo apt install lm-sensors` -> `sudo sensors-detect` -> `sudo sensors` (sensors in console)
   1. [Google Chrome](https://www.google.com/intl/ru_ru/chrome/). Download `DEB` package and start installation
      1. To set as default browser go to `System Settings > Applications > Default Applications > Web Browser`
   1. [Skype](https://www.skype.com/ru/get-skype/)
   1. [Telegram](https://desktop.telegram.org/)
   1. qBittorrent: `sudo apt install qbittorrent`
   1. [IntellijIdea(see 2020.1.1)](https://www.jetbrains.com/ru-ru/idea/download/#section=linux), [treatment](https://rutracker.org/forum/viewtopic.php?t=5883972)
      1. `tar -xzvf ideaIU-2020.1.tar.gz`
      1. `sudo mkdir -p /opt/jetbrains/idea`
      1. `sudo mv ~/Downloads/idea-IU-201.6668.121/ /opt/jetbrains/idea/idea-2020.1`
      1. `sudo /opt/jetbrains/idea/idea-2020.1/bin/idea.sh`
   1. [Visual Studio Code](https://code.visualstudio.com/download)
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
      1. `export JAVA_HOME=/usr/lib/jvm/jdk-14.0.2`
      1. `sudo update-alternatives --install /usr/bin/java java ${JAVA_HOME}/bin/java 2000`
      1. `sudo update-alternatives --install /usr/bin/javac javac ${JAVA_HOME}/bin/javac 2000`
      1. `sudo update-alternatives --install /usr/bin/javap javap ${JAVA_HOME}/bin/javap 2000`
      1. `sudo update-alternatives --install /usr/bin/jar jar ${JAVA_HOME}/bin/jar 2000`
      1. `sudo update-alternatives --install /usr/bin/keytool keytool ${JAVA_HOME}/bin/keytool 2000`
      1. `sudo update-alternatives --install /usr/bin/jarsigner jarsigner ${JAVA_HOME}/bin/jarsigner 2000`      
      1. `sudo update-alternatives --install /usr/bin/jstat jstat ${JAVA_HOME}/bin/jstat 2000`
      1. `sudo update-alternatives --install /usr/bin/jmap jmap ${JAVA_HOME}/bin/jmap 2000`
      1. `sudo update-alternatives --install /usr/bin/jstack jstack ${JAVA_HOME}/bin/jstack 2000`
      1. `sudo update-alternatives --install /usr/bin/jfr jarsigner ${JAVA_HOME}/bin/jfr 2000`      
      1. `sudo update-alternatives --install /usr/bin/jjs jarsigner ${JAVA_HOME}/bin/jjs 2000`      
      1. check `sudo update-alternatives --config java`      
      1. ```sudo sh -c 'echo "export JAVA_HOME='"${JAVA_HOME}"'" >> /etc/profile' && source /etc/profile``` 
          **OR**
          ```echo "export JAVA2_HOME=${JAVA_HOME}" >> ~/.profile && source ~/.profile```
      1. restart   
   1. AdoptJDK: https://adoptopenjdk.net/installation.html#linux-pkg       
   1. [Maven](http://maven.apache.org). [How to install](https://www.apache-maven.ru/install.html): 
      1. `export ver=3.6.3`
      1. `mkdir -p ~/Downloads`
      1. `wget  -O ~/Downloads/apache-maven-${ver}-bin.tar.gz https://dlcdn.apache.org/maven/maven-3/${ver}/binaries/apache-maven-${ver}-bin.tar.gz`
         1. or download manually: http://maven.apache.org/download.html
      1. `sudo mkdir -p /opt/maven && sudo cp /home/$USER/Downloads/apache-maven-*.tar.gz /opt/maven`
      1. `sudo tar -xvf "/opt/maven/apache-maven-${ver}-bin.tar.gz" -C /opt/maven/`
      1. `sudo sh -c 'echo "export M2_HOME=/opt/maven/apache-maven-'"${ver}"'" >> /etc/profile' && source /etc/profile`
         **OR**
         `echo "export M2_HOME=/opt/maven/apache-maven-${ver}" >> ~/.profile && source ~/.profile`
      1. `sudo update-alternatives --install /usr/bin/mvn mvn "${M2_HOME}/bin/mvn" 120`
      1. check `sudo update-alternatives --config mvn`
      1. restart
         1. [Bash completions](https://github.com/juven/maven-bash-completion) 
   1. node/npm
      1. [Установить node через пакетный менеджер](https://nodejs.org/ru/download/package-manager/). Выбрать nvm или nvs для windows.
         1. В Windows 11: `winget install jasongin.nvs`. Use `nvs link <version>` to use some version permanentally
      1. `nvm install 10.13.0`
      2. to switch version call: `nvm use 16.17.1 && nvm alias default 16.17.1`
      3. `npm set editor mcedit`
      4. `npm config set @mycorp:registry "<corp-registry-url>"`
      5. See subtle configuration here: https://gist.github.com/gorshkov-leonid/b55072d6876acecf43dabaf7f1e72cf0#configuration
   1. [docker](https://docker.com)
      1. [Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/). Better to use repositories.
      1. [post-install](https://docs.docker.com/engine/install/linux-postinstall/#manage-docker-as-a-non-root-user)
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
             export COMM=
             for i in "${@:2}"; do
               case "$i" in
                   *\'*)
                       export COMM="$COMM \"$i\""
                       ;;
                   *) 
                       export COMM="$COMM '$i'"
                   ;;              
               esac
             done
    
             if [ "$1" == "build" ]; then
                 bash -c 'command docker '"$1 --network host $COMM"
             else
                 bash -c 'command docker '"$1 $COMM"
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
 1. Scripts
    1. Find process by port `nsenter -n/proc/11021/ns/net netstat -tulpn`     
   
Useful Links:
* [13 Keyboard Shortcut Every Ubuntu 18.04 User Should Know](https://itsfoss.com/ubuntu-shortcuts/)
* https://github.com/moby/moby/issues/23910#issuecomment-247964052
* https://github.com/moby/moby/issues/23910#issuecomment-390268678
* https://github.com/docker/for-linux/issues/979 and https://github.com/moby/moby/pull/41022
* touch /etc/NetworkManager/dnsmasq.d/docker-bridge.conf
* echo 'listen-address=_*2.168.1*9.0' | sudo tee -a '/etc/NetworkManager/dnsmasq.d/docker-bridge.conf'

