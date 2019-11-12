---
layout: post
title:  "How to setup key pair for Linux"
categories: Operation
tags:  Linux
excerpt: null
mathjax: true
author: Bo Chen
---
* content
{:toc}

### Generate SSH key
	ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
	
<https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/>
	
### Create a user in target env and authenticate by public key
- `useradd username`
- `cd etc/ssh`
- `cp sshd_configure sshd_configure.backup`
- enable the public key authentication
- `service sshd restart`
- `service sshd status`
- `vim ~/.ssh/authorized_keys`
- append the public key to the keys file
- `usermod -a -G groupname username`
	
### Save the private key to Jenkins and called by pipeline