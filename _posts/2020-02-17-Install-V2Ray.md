---
layout: post
title:  "Install V2Ray in CentOS"
categories: Network
tags:  Firewall
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

  * `# bash <(curl -L https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-release.sh)`

* Set it running as service.
  
``` shell
systemctl enable v2ray
systemctl start v2ray
systemctl status v2ray
systemctl stop v2ray
systemctl restart v2ray
```

* Check the configuration

  * Sample https://github.com/v2fly/v2ray-examples

  * Check the console output during the script running for the config file name
  
  * Another way to find the config file name `systemctl status v2ray`

* Setup the client
  
  * IOS - Shadowrocket
  * Mac - V2RayU - https://github.com/yanue/V2rayU
  * Win - V2RayN - https://github.com/2dust/v2rayN 
  * Others - https://www.v2ray.com/awesome/tools.html
