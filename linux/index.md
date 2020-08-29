* Восстановление файловой системы: fsck -fy -t ext4 /dev/sda1
* Имя текущего пользователя `id -un`
* Версия системы `lsb_release -a`
* network
   * `sudo sed -i 's/^dns=dnsmasq/#&/' /etc/NetworkManager/NetworkManager.conf` 
   * `sudo service network-manager restart`
   * `sudo service networking restart`
   * `sudo sysctl -w net.ipv4.tcp_max_syn_backlog 16000` максимальное кол-во соединений (на постоянку `/etc/sysctl.conf`)
* nmcli
   * [Управляем сетевыми подключениями в Linux с помощью консольной утилиты nmcli](https://habr.com/ru/company/vdsina/blog/512282/)
   * `nmcli dev show | grep DNS` - current dns
   * sudo nmcli networking off && sudo nmcli networking on -restart nm
  

