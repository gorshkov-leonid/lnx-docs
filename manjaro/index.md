* VPN
  * Installation problem: [Arch AnyConnect VPN installation issues.](https://bbs.archlinux.org/viewtopic.php?id=237621). 
     1. `cd ~/Downloads`
     2. `sudo chmod 777 ./anyconnect-linux64-4.6.04056-core-vpn-webdeploy-k9.sh`    
     3.  `sudo ln -s /etc/systemd/system /etc/rc.d`
     4. Create Unit `vpnagentd.service`
     ```  
     sudo echo -e "[Service] 
     Type=simple
     ExecStart=/etc/systemd/user/vpnagentd start
     ExecStop=/etc/systemd/user/vpnagentd stop
     Restart=on-failure

     [Install]
     WantedBy=multi-user.target" | sudo tee /etc/systemd/system/vpnagentd.service
     ```
     5. `sudo ./anyconnect-linux64-4.6.04056-core-vpn-webdeploy-k9.sh`
     6.  `systemctl status vpnagentd`
* TBD     
