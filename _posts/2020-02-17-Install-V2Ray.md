---
layout: post
title:  "Install V2Ray in CentOS"
categories: Miscellaneous
tags:  Misc
excerpt: null
mathjax: true
author: Bo Chen
---

* content
{:toc}

## Install V2Ray on CentOS

* Preparation
  * Following instruction verified on CentOS 8
  * Website - https://www.v2ray.com/
  * Official guide - https://www.v2ray.com/chapter_00/install.html

* Download and install from the script.

  * `bash <(curl -L -s https://install.direct/go.sh)`

* Set it running as service.
  
``` shell
systemctl enable v2ray

systemctl start v2ray

systemctl status v2ray

systemctl stop v2ray

systemctl restart v2ray
```

* Check the configuration

  `cat /etc/v2ray/config.json`

  * you can also check the console output during the script running

* Setup the client
  
  * IOS - Shadowrocket
  * Mac - V2RayU - https://github.com/yanue/V2rayU
  * Win - V2RayN - https://github.com/2dust/v2rayN 
  * Others - https://www.v2ray.com/awesome/tools.html
