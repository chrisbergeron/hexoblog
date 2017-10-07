---
title: Inxi - a utility for viewing system information
date: 2017/10/07 20:46:25
tags:
  - inxi
  - devops
category:
  - linux
thumbnail: images/tech/Bash-new.sh-600x600.png
---
## Inxi
[inxi](https://smxi.org/docs/inxi.htm) is a super handy system info utility.  These days I typically work with ephemeral instances / microservers, so I just dispose of infrastructure that flakes out.  Occassionally I'll need to see what's up with a box so I've put together some common invocations of inxi below for reference:

### Common Invocations

**General system info:**
```bash
$ ./inxi -c 5 -b

System:    Host: mgmt-01.tools.atl.primedia.com Kernel: 3.10.0-229.el7.x86_64 x86_64 bits: 64 Console: tty 4
           Distro: Scientific Linux release 7.1 (Nitrogen)
Machine:   Device: vmware System: VMware product: VMware Virtual Platform serial: VMware-42 01 09 7b d7 cf ec cd-a6 9a 79 d9 35 f5 0c 95
           Mobo: Intel model: 440BX Desktop Reference Platform serial: N/A BIOS: Phoenix v: 6.00 date: 09/17/2015
CPU(s):    2 Single core Intel Xeon E5-2698 v3s (-HT-SMP-) speed: 2294 MHz (max)
Graphics:  Card: VMware SVGA II Adapter
           Display Server: N/A driver: vmwgfx tty size: 180x50 Advanced Data: N/A for root out of X
Network:   Card: VMware VMXNET3 Ethernet Controller driver: vmxnet3
Drives:    HDD Total Size: 96.6GB (20.1% used)
Info:      Processes: 132 Uptime: 439 days Memory: 398.0/3792.0MB Init: systemd runlevel: 3
           Client: Shell (bash) inxi: 2.3.39
```

**Full system info:**
``` bash
$ ./inxi -Fi

System:    Host: mgmt-01.tools.atl.primedia.com Kernel: 3.10.0-229.el7.x86_64 x86_64 bits: 64 Console: tty 4
           Distro: Scientific Linux release 7.1 (Nitrogen)
Machine:   Device: vmware System: VMware product: VMware Virtual Platform serial: VMware-42 01 09 7b d7 cf ec cd-a6 9a 79 d9 35 f5 0c 95
           Mobo: Intel model: 440BX Desktop Reference Platform serial: N/A BIOS: Phoenix v: 6.00 date: 09/17/2015
CPU(s):    2 Single core Intel Xeon E5-2698 v3s (-HT-SMP-) cache: 81920 KB
           clock speeds: max: 2294 MHz 1: 2294 MHz 2: 2294 MHz
Graphics:  Card: VMware SVGA II Adapter
           Display Server: N/A driver: vmwgfx tty size: 180x50 Advanced Data: N/A for root out of X
Network:   Card: VMware VMXNET3 Ethernet Controller driver: vmxnet3
           IF: eth0 state: up speed: 10000 Mbps duplex: full mac: 00:50:56:81:59:7e
           WAN IP: 216.52.38.4
           IF: eth0 ip-v4: 172.24.107.75 ip-v6-link: fe80::250:56ff:fe81:597e
Drives:    HDD Total Size: 96.6GB (20.1% used)
           ID-1: /dev/sda model: Virtual_disk size: 21.5GB
           ID-2: /dev/sdb model: Virtual_disk size: 75.2GB
Partition: ID-1: / size: 88G used: 17G (19%) fs: xfs dev: /dev/dm-1
           ID-2: /boot size: 497M used: 89M (18%) fs: xfs dev: /dev/sda1
           ID-3: swap-1 size: 2.15GB used: 0.10GB (5%) fs: swap dev: /dev/dm-0
RAID:      No RAID devices: /proc/mdstat, md_mod kernel module present
Sensors:   None detected - is lm-sensors installed and configured?
Info:      Processes: 132 Uptime: 439 days Memory: 397.8/3792.0MB Init: systemd runlevel: 3
           Client: Shell (bash) inxi: 2.3.39
```

**View repos:**
```bash
$ ./inxi -r
```
Repos:     Active yum sources in file: /etc/yum.repos.d/spacewalk-client.repo
           spacewalk-client ~ http://yum.spacewalkproject.org/2.2-client/RHEL/7/$basearch/
```

The inxi code base is (here)[https://github.com/smxi/inxi].
