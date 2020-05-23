* VPN
  * [Arch AnyConnect VPN installation issues.](https://bbs.archlinux.org/viewtopic.php?id=237621) :-(
  * не помогло
  ``` 
  pacman -S networkmanager-vpnc
  pacman -S networkmanager-openconnect
  pacman -S networkmanager-openvpn
  ````
  * `openconnect corp.com` => `Server asked us to run CSD hostscan`: https://gist.github.com/l0ki000/56845c00fd2a0e76d688
  * https://together.jolla.com/question/218981/openconnect-with-second-factor-auth-is-not-possible-sfos-321/
