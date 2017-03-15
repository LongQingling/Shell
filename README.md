## Linux Shell for ARM(imx6)


#### [1] ME909s821_ECM
  
$  
  
#### [2] Configure service
  
$vim configure.service 
[Unit]  
Description=Pbox configure service.  
After=multi-user.target  
  
[Service]  
Type=oneshot  
ExecStart=/etc/pboxConfigure.sh  
[Install]  
WantedBy=multi-user.target  
  
#### [3] pbox_daemon
  
$vim wireless_lte.service  
  
[Unit]  
Description=Pbox LTE(4G) Daemon Shell  
After=multi-user.target `configure.service`  
  
[Service]  
Type=`simple`  
ExecStart=/home/wireless_lte_daemon.sh  
[Install]  
WantedBy=multi-user.target  
  
$systemctl enable wireless_lte.service  
$vim cora.timer  
  
[Unit]  
Description=Runs Pbox Script every 2 min  
  
[Timer]  
OnBootSec=1min  
OnUnitActiveSec=`2min`  
Unit=`wireless_lte.service`  
  
[Install]  
WantedBy=multi-user.target  
  
$systemctl enable cora.timer  
$systemctl start cora.timer  
