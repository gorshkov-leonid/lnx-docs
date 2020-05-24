* VPN
  * Installation problem: [Arch AnyConnect VPN installation issues.](https://bbs.archlinux.org/viewtopic.php?id=237621). 
     a. `chmod 777 ./anyconnect-linux64-4.6.04056-core-vpn-webdeploy-k9.sh`
     b. `./anyconnect-linux64-4.6.04056-core-vpn-webdeploy-k9.sh`
       * Expected error: `cannot create regular file '/etc/rc.d/vpnagentd': No such file or directory`
       * See where it was extracted to: `Unarchiving installation files to /tmp/vpn.E8RrUl...`
       * Set this value to variable CAC_TMP=/tmp/vpn.E8RrUl
     c. `sudo chmod 777 $CAC_TMP && mkdir ~/CiscoAnyConnectDist && sudo cp -r $CAC_TMP/vpn/* ~/CiscoAnyConnectDist && cd ~/CiscoAnyConnectDist`
     d.  `sudo ./vpn_install.sh`
       * Expected error the same: `install: cannot create regular file '/etc/rc.d/vpnagentd': No such file or directory`
     e.  `sudo ln -sf /etc/systemd/system /etc/rc.d/ && sudo ./vpn_install.sh`
       * Expected error: `Failed to start vpnagentd.service: Unit vpnagentd.service not found.` 
     f. Create Unit `vpnagentd.service`
     ```  
     sudo echo -e "[Service] 
     Type=oneshot
     RemainAfterExit=yes
     ExecStart=/etc/systemd/user/vpnagentd start
     ExecStop=/etc/systemd/user/vpnagentd stop
     Restart=on-failure

     [Install]
     WantedBy=multi-user.target" | sudo tee /etc/systemd/system/vpnagentd.service
     ```
     1. 
     1. aaa
    
  sudo ./vpn_install.sh
  systemctl stop vpnagentd.service
  systemctl status vpnagentd.service
  systemctl stop vpnagentd.service
  

  
  не помогло
  ``` 
  pacman -S networkmanager-vpnc
  pacman -S networkmanager-openconnect
  pacman -S networkmanager-openvpn
  ````
  * `openconnect corp.com` => `Server asked us to run CSD hostscan`: https://gist.github.com/l0ki000/56845c00fd2a0e76d688
  * https://together.jolla.com/question/218981/openconnect-with-second-factor-auth-is-not-possible-sfos-321/
  * https://unix.stackexchange.com/questions/449174/connman-how-to-set-up-openconnect-vpn-with-csd-wrapper-correctly
