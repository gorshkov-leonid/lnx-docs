* Восстановление файловой системы: fsck -fy -t ext4 /dev/sda1
* Имя текущего пользователя `id -un`
* network
   * `sudo sed -i 's/^dns=dnsmasq/#&/' /etc/NetworkManager/NetworkManager.conf` 
   * `sudo service network-manager restart`
   * `sudo service networking restart`
