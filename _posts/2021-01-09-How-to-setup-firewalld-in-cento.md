---
layout: post
title:  "How to setup firewalld in centos"
categories: Operation
tags:  Linux firewalld
excerpt: null
mathjax: true
author: Internet
---

* content
{:toc}

In order to make our website is accessable, we need to open the service or port from the firewall. In this article, we will whow how to set up a firewall for your server and show you the basics of the firewall-cmd tool.

## Basic concepts

### Zone

In order from least trusted to most trusted, the predefined zones within firewalld are:

* drop: The lowest level of trust. All incoming connections are dropped without reply and only outgoing connections are possible.
* block: Similar to the above, but instead of simply dropping connections, incoming requests are rejected with an icmp-host-prohibited or icmp6-adm-prohibited message.
* public: Represents public, untrusted networks. You don’t trust other computers but may allow selected incoming connections on a case-by-case basis.
* external: External networks in the event that you are using the firewall as your gateway. It is configured for NAT masquerading so that your internal network remains private but reachable.
* internal: The other side of the external zone, used for the internal portion of a gateway. The computers are fairly trustworthy and some additional services are available.
* dmz: Used for computers located in a DMZ (isolated computers that will not have access to the rest of your network). Only certain incoming connections are allowed.
* work: Used for work machines. Trust most of the computers in the network. A few more services might be allowed.
* home: A home environment. It generally implies that you trust most of the other computers and that a few more services will be accepted.
* trusted: Trust all of the machines in the network. The most open of the available options and should be used sparingly.

### Rule Permanence

* `--permanent` flag to indicate that the non-ephemeral firewall should be targeted.

## Install and Enable Your Firewall to Start at Boot

* `sudo yum install firewalld`
* `sudo systemctl enable firewalld`
* `sudo reboot`
* Verify the status `sudo firewall-cmd --state`

## Get the Current Firewall Rules

### Check the Defaults

* Get the Default zone `firewall-cmd --get-default-zone`
* Get the “active” zone (the zone that is controlling the traffic for our interfaces). `firewall-cmd --get-active-zones`
* Get the rules associated with the public zone `sudo firewall-cmd --list-all`

### Check Alternative Zones

* Get a list of the available zones `firewall-cmd --get-zones`
* Check the specific configuration associated with a zone `sudo firewall-cmd --zone=home --list-all`
* Check all zones `sudo firewall-cmd --list-all-zones | less`

## Selecting Zones for your Interfaces

### Changing the Zone of an Interface

* Transition our eth0 interface to the “home” zone `sudo firewall-cmd --zone=home --change-interface=eth0`
* Verify the transition `firewall-cmd --get-active-zones`

### Adjusting the Default Zone

* Change the default zone `sudo firewall-cmd --set-default-zone=home`

## Setting Rules for your Applications

### Adding a Service to your Zones

* Get a list of the available services `firewall-cmd --get-services`
  * You can get more details about each of these services by looking at their associated .xml file within the /usr/lib/firewalld/services directory.
* Allow the traffice for HTTP service `sudo firewall-cmd --zone=public --add-service=http`
* Modify the permanent firewall rules so that your service will still be available after a reboot `sudo firewall-cmd --zone=public --permanent --add-service=http`
* Verify successful adding the --permanent flag `sudo firewall-cmd --zone=public --permanent --list-services`
* Add the https service
  * `sudo firewall-cmd --zone=public --add-service=https`
  * `sudo firewall-cmd --zone=public --permanent --add-service=https`

### What If No Appropriate Service Is Available?

* Opening a Port for your Zones Protocols can be either tcp or udp `sudo firewall-cmd --zone=public --add-port=5000/tcp`
* Verify that this was successful `sudo firewall-cmd --zone=public --list-ports`
* Specify a sequential range of ports `sudo firewall-cmd --zone=public --add-port=4990-4999/udp`
* Add these to the permanent firewall.
  * `sudo firewall-cmd --zone=public --permanent --add-port=5000/tcp`
  * `sudo firewall-cmd --zone=public --permanent --add-port=4990-4999/udp`
  * `sudo firewall-cmd --zone=public --permanent --list-ports`

### Defining a Service

* For instance, we could copy the SSH service definition to use for our “example” service `sudo cp /usr/lib/firewalld/services/ssh.xml /etc/firewalld/services/example.xml`
* Adjust the definition `sudo vi /etc/firewalld/services/example.xml`
* Reload your firewall to get access to your new services `sudo firewall-cmd --reload`
* List available services `firewall-cmd --get-services`

## Creating Your Own Zones

* Create the two zones:
  * `sudo firewall-cmd --permanent --new-zone=publicweb`
  * `sudo firewall-cmd --permanent --new-zone=privateDNS`
* Verify your permanent configuration `sudo firewall-cmd --permanent --get-zones`
* Reload the firewall
  * `sudo firewall-cmd --reload`
  * `firewall-cmd --get-zones`
* Assigning the appropriate services and ports to your zones.
  * `sudo firewall-cmd --zone=publicweb --add-service=ssh`
  * `sudo firewall-cmd --zone=publicweb --add-service=http`
  * `sudo firewall-cmd --zone=publicweb --add-service=https`
  * `sudo firewall-cmd --zone=publicweb --list-all`
* Add the DNS service to our “privateDNS” zone:
  * `sudo firewall-cmd --zone=privateDNS --add-service=dns`
  * `sudo firewall-cmd --zone=privateDNS --list-all`
* Change our interfaces over to these new zones to test them out
  * `sudo firewall-cmd --zone=publicweb --change-interface=eth0`
  * `sudo firewall-cmd --zone=privateDNS --change-interface=eth1`
* Add the same rules to the permanent configuration.
  * `sudo firewall-cmd --zone=publicweb --permanent --add-service=ssh`
  * `sudo firewall-cmd --zone=publicweb --permanent --add-service=http`
  * `sudo firewall-cmd --zone=publicweb --permanent --add-service=https`
  * `sudo firewall-cmd --zone=privateDNS --permanent --add-service=dns`
* Restart your network and reload your firewall service
  * `sudo systemctl restart network`
  * `sudo systemctl reload firewalld`
* Validate that the correct zones were assigned `firewall-cmd --get-active-zones`
* Validate that the appropriate services are available for both of the zones
  * `sudo firewall-cmd --zone=publicweb --list-services`
  * `sudo firewall-cmd --zone=privateDNS --list-services`
* make one of these zones the default for other interfaces `sudo firewall-cmd --set-default-zone=publicweb`

## References

* <https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-using-firewalld-on-centos-7>
