---
layout: post
title:  "How to manage proxy in chrome"
categories: Miscellaneous
tags:  Misc
excerpt: null
mathjax: true
author: Bo Chen
---

* content
{:toc}

## Install SwitchyOmega plugin

SwitchOmega is a tool to manage and switch between multiple proxies quickly & easily.

* You can try it on Chrome Web Store<https://chrome.google.com/webstore/detail/padekgcemlokbadohgkifijomclgjgif>, or grab a packaged extension file (CRX) for offline installation on the Releases page of the git repo.
* Git repo: <https://github.com/FelisCatus/SwitchyOmega>

## Config the plugin

* Create proxy profiles mapping to different proxy
* Create switch profiles to map to proxy profile
* Setup rules in the switch profile
* Setup the rulelist config
  * Choose `AutoProxy`
  * Rulelist url: <https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt>

For more details, please refer <http://junch.github.io/%E6%8A%80%E5%B7%A7/2015/06/05/original-proxy.html>
