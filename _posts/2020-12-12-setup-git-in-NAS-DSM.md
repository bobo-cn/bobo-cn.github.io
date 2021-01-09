---
layout: post
title:  "Setup SSH and git in NAS"
categories: NAS
tags:  SSH Git DSM Linux NAS Synology
excerpt: null
mathjax: true
author: Bo Chen
---

* content
{:toc}

### Setup SSH and make it pubkey authenticate

* Config a host alia nas.local
  * `vi /etc/hosts`
  * Add a line `192.168.x.x  nas.local`
  * `:w!q`
  * verify the result by `ping nas.local`
* Enable the SSH service in console
  * Log into DSM using an account with administrative privileges. Go to Control Panel > Terminal and enable SSH service.
* Enable the pubkey authenticate
  * check and ensure the "pubkey authentication" is enabled
    * ssh to nas `ssh nas.local`
    * `cat /etc/ssh/sshd_config | grep Pubkey`
    * ensure the value is yes and working
    * restart the ssh if changed the configure
      * `sudo synoservicectl --reload sshd`
* Import the SSH Key to nas
  * `ssh-copy-id -i xxx.ssh user@nas.local`
  * Check the permission
    * home: 755
    * .ssh: 700
    * autherized_keys: 600
* Verify the result
  * `ssh user@nas.local`
  * trouble shooting
    * run from nas: `sudo /bin/sshd -d -p 1234`
    * run from local: `ssh user@nas.local -p 1234`

### Install the git server

* Launch the Git package. Select users to provide them with the ability to check in and check out files from the repository.
  * If the panel is blank, try following
    * `sudo vi /var/packages/Git/target/webapi/SYNO.Git.lib`
    * delete the content within appPriv: -> "appPriv": ""
* Log into your Synology server via SSH as root or admin.
* Change directory to /volumeX, where X is the volume number, to create a folder. For example, "git_repos". The permission of the folder will be the same as Linux.
  * You can also do it in web console
* In the folder, run git init to create an empty repository.
  * `git init --bare <repo.git>`
* After the repository is created, a Git client user can enter the following command to access this repository:
  * `git clone ssh://[Git users]@[Your Synology server's IP address or hostname]/[Git repository path]`
    * `git clone ssh://user@nas.local/volume1/git/test1.git`
    * ensure it starts from **ssh://**
    * You can also use the scp like style `git clone [git_user]@nas.local:/volume1/git/helloworld.git`
    * If you are using a port other than 22, update following
      * `vi ~/.ssh/config`

      ``` bash
      Host nas.local
      Port 1234
      ```
