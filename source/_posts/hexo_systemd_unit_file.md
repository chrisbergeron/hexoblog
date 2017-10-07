---
title: A systemD unit file for Hexo
date: 2017/10/07 20:46:25
tags:
  - systemd
  - hexo
category:
  - blog
thumbnail: https://raw.githubusercontent.com/hexojs/awesome-hexo/master/hexo-logo.png
---
[Hexo](https://hexo.io/) is a simple, lightweight node blog framework. It didn't include a SystemD Unit file, so I created one:

## Hexo SystemD Unit File

### /lib/system/systemd/hexo.service

```bash
[Service]
WorkingDirectory=/home/[yourdirectory]/blog
ExecStart=/bin/hexo server -p80
Restart=always
StandardOutput=syslog
StandardError=syslog
SyslogIdentifier=hexo
User=root
Group=root
Environment=NODE_ENV=production

[Install]
WantedBy=multi-user.target
```
Obviously, you'll want to replace [yourdirectory] with the location of your Hexo blog.

### Start Hexo
``` bash
$ sudo systemctl start hexo
```

### View status of Hexo
``` bash
$ sudo systemctl status hexo
● hexo.service
   Loaded: loaded (/usr/lib/systemd/system/hexo.service; disabled; vendor preset: disabled)
   Active: active (running) since Sat 2017-10-07 02:27:36 UTC; 7min ago
 Main PID: 8997 (hexo)
   CGroup: /system.slice/hexo.service
           └─8997 hexo

Oct 07 02:27:36 centos-2gb-nyc1-01 systemd[1]: Started hexo.service.
Oct 07 02:27:36 centos-2gb-nyc1-01 systemd[1]: Starting hexo.service...
Oct 07 02:27:38 centos-2gb-nyc1-01 hexo[8997]: INFO  Start processing
Oct 07 02:27:38 centos-2gb-nyc1-01 hexo[8997]: INFO  Hexo is running at http://localhost:80/. Press Ctrl+C to stop.
```
I recommend [Digital Ocean](http://pages.news.digitalocean.com/dc/AyKQ30vur1Nt8H30LIWxk-j5xHmafGnoECQwn1ooO77yBt0FNL3mSORKe-qOjqAUuFeCU3DjjCwgDxcGj4qztQ==/v1U40XUb0V6DEYm0I03k000) for great cloud hosting.

