---
title: System info bash script
date: 2017/10/07 20:46:25
tags:
  - bash
  - devops
category:
  - linux
thumbnail: http://67.205.170.54:8989/Content/Images/logos/128.png
---

I put together a quick bash shell script to view system info at a glance.  I know there are existing tools for this like [inxi](https://smxi.org/docs/inxi.htm), but I wanted to put something together I can copypasta.  This is specific to RHEL, Centos and Sci Linux but it can be easily adapted for other distros.

```bash
#!/bin/bash

# run as root

#echo "================================ Services: ================================"
#for i in `journalctl -F _SYSTEMD_UNIT | grep -v session | sed -e "s/.service//g"`; do echo "========= $i ========="; ps aux | grep -v grep | grep $i; done

echo "================================ Service restarts today: ====================================="
output=`journalctl --since today | grep -v slice | egrep "Starting|Stopping" | grep -v systemd`
echo "$output"

echo "================================ User logins today: =========================================="
output=`journalctl --since today | grep -v slice | grep pam_unix`
echo "$output"

echo "================================ Non core processes: ========================================="
pstree -n | grep -v lvmeta | grep -v systemd | grep -v rhn | grep -v dbus-daemon | grep -v crond | grep -v agetty | grep -v oddjobd | grep -v vmtoolsd | grep -v tuned | grep -v rsyslog | grep -v irqbalance | grep -v ntpd | grep -v sssd | grep -v qmgr | grep -v pickup | grep -v puppet | grep -v mcollectived | grep -v dhclient | grep -v sshd | grep -v nrpe | grep -v collectd | grep -v xinetd | grep -v consul | grep -v rpcbind | grep -v grep

echo "================================ Open ports: ================================================="
sudo netstat -ntpl | grep -v ssh | grep -v nrpe | grep -v master | grep -v "rpc" | grep -v Active | grep -v Proto | grep -v xinetd | grep -v systemd | sed -e "s/:::/0.0.0.0:/g" | tr -s " " | cut -f4,7- -d " "

echo "================================ Open Sockets: ==============================================="
sudo systemctl list-sockets
echo "================================ Uptime: ====================================================="
uptime
echo "================================ Users: ======================================================"
who
echo "================================ Volume Info: ================================================“
lvdisplay | grep "LV Name"
vgdisplay | grep "VG Name"
```
