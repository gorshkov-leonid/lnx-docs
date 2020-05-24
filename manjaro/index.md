* VPN
  * Installation problem: [Arch AnyConnect VPN installation issues.](https://bbs.archlinux.org/viewtopic.php?id=237621). 
     1. `cd ~/Downloads`
     2. `sudo chmod 777 ./anyconnect-linux64-4.6.04056-core-vpn-webdeploy-k9.sh`    
     3.  `sudo ln -s /etc/systemd/user /etc/rc.d`
     4. Create Unit `vpnagentd.service`
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
     5. `systemctl daemon-reload`
     6. `sudo ./anyconnect-linux64-4.6.04056-core-vpn-webdeploy-k9.sh`
     7.  `systemctl status vpnagentd`
* TBD     
