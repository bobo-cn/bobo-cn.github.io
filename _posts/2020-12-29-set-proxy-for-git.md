---
layout: post
title:  "Set proxy for git"
categories: Network
tags:  Firewall Git
excerpt: null
mathjax: true
author: Bo Chen
---

* content
{:toc}

## Why we need to setup proxy for git

For those machine behind the firewall

## Two ways to setup the proxy

### Setup the proxy for http protocol

* Add a single proxy for all
`git config --global http.proxy http://proxyUsername:proxyPassword@proxy.server.com:port`

* Add proxy for different hosts

``` bash
git config --global http.https://domain.com.proxy http://proxyUsername:proxyPassword@proxy.server.com:port
git config --global http.https://domain.com.sslVerify false
```

* Check <https://gist.github.com/evantoli/f8c23a37eb3558ab8765> for more details.
* Only works for `git clone https://xxxxx`

### Setup the proxy for git protocol

* Windows only
  * `vim ~/.ssh/config`
  * Update the content as following, -S means sock proxy. Http proxy not work at the moment
  
  ``` bash
    # Global setting
    # ProxyCommand connect -S 127.0.0.1:6600 %h %p
    # For specific host
      Host github.com
        ProxyCommand connect -S 127.0.0.1:6600 %h %p
  ```

  * Refer <https://blog.csdn.net/w8y56f/article/details/102565809> for more details.
  * Use ssh tunnel to setup the sock proxy

* For mac, refer <https://serverfault.com/questions/315605/ssh-through-a-socks-proxy-client-openssh-os-x>
  * update `~/.ssh/config`
  * "5" is the SOCKS version, "1080" is the proxy port, "%h" SSH replaces with the host you typed on the command line, and "%p" SSH replaces with the port from the command line (or the default 22).

``` bash
  Host 10.*
    ProxyCommand nc -X 5 -x PROXY_HOST:1080 %h %p
```
