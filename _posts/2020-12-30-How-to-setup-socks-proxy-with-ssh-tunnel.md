---
layout: post
title:  "How to setup socks proxy with ssh tunnel"
categories: Network
tags:  Firewall
excerpt: null
mathjax: true
author: Bo Chen
---

* content
{:toc}

A SOCKS proxy is an SSH encrypted tunnel in which configured applications forward their traffic down, and then, on the server-end, the proxy forwards the traffic to the general Internet. Unlike a VPN, a SOCKS proxy has to be configured on an app-by-app basis on the client machine, but you can set up apps without any specialty client software as long as the app is capable of using a SOCKS proxy. On the server-side, all you need to configure is SSH.

## Setup ssh tunnel with cli on your local machine

`ssh -i ~/.ssh/id_rsa -D 1337 -f -C -q -N user@your_domain`

* Explanation of arguments
  * `-i`: The path to the SSH key to be used to connect to the host
  * `-D`: Tells SSH that we want a SOCKS tunnel on the specified port number (you can choose a number between 1025 and 65536)
  * `-f`: Forks the process to the background
  * `-C`: Compresses the data before sending it
  * `-q`: Uses quiet mode
  * `-N`: Tells SSH that no command will be sent once the tunnel is up

## Setup tunnel with putty on windows

* Open putty and make it working for ssh to the remote
* In `“Connection”→“SSH”→“Tunnels”`, setup the following
  * `source port`, need larger than 1024
  * select `Dynamic`
  * push the button `add`
* Connect to remote and enjoy!  
* For more details, please refer <http://junch.github.io/%E6%8A%80%E5%B7%A7/2015/06/05/original-proxy.html>
