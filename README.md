w
Description
===========

"Whitehole" is IaaS Platform based on KVM and Libvirt-PHP.

### Notice

* (I'm beginning PHP, so it is very helpful if help me clean up the source code .)
* Prototype level, exception handling is weak.
* Single management node and many KVM-Based computing nodes.
* Simultaneous, multi-processing considerations weak.
* Source code is not clean yet.
* Private-IP per tenant assignments are not yet considered. (Directly Public-IP like AWS EC2)
* Default Template: Ubuntu Server 13.04 x86_64 (Compressed qcow2 Image, about 320MB)
* Xen-hypervisor is not support yet.
* Windows-VM is not support yes.

Screenshot
==========

Click to view.

[![VM List](https://raw.github.com/call518/whitehole/master/screenshot/screenshot-whitehole-1.PNG)](https://raw.github.com/call518/whitehole/master/screenshot/screenshot-whitehole-1.PNG)

Feature
=======

* VM Instance: Create(from Template/ISO)/Delete/On/Off/Reboot
* SSH-Keypair
* Live-Migration
* Monitoring: Traffic/Packet/CPU/DiskIO(Byte/Count)
* root-Volume Resizing.
* 2nd-Volume (not like EBS, Can not online attache/detache)
* Security Group
* Snapshot (Current Can not Live, Require Reboot)
* Custom Template Image: Create(from Snapshot)/Delete/Create New VM(from Custom Template)
* Privat-DNS: Hostname.test.org <-> IP-Address
* Primary Storage: for VM HDD Image
* Secondary Storage: Template/SSH-Keypair/Etc...


Platform Requirement
====================

* Ubuntu Server 13.04 (x86_64)
* KVM Hypervisor
* NFS Storage (Primary/Secondary)
* MRTG/SNMP/Etc..
* Recommended Web-Browser: Google Chrom

Software
========

### Ubuntu Packages

* apache2
* php
* mysql
* libvirt
* qemu-utils
* kpartx

### External Solution

* libvirt-php
* ssh2 (No longer needed...)
* jquery-ui

Directory
=========

### whitehole-home

* Destination DIR: /home/whitehole
* Cron, Monitoring, MRTG-Template, DDNS, Etc...

### whitehole-html

* Destination DIR: /var/www/html
* PHP Sources, MySQL Schema, OpenSource-Board, Etc...

Installation
============

### Support Auto Install-Script

* Mamangement Server: setup-mgm.sh (Should be executed before setup-node.sh)
* Physical Compute Node: setup-node.sh

### Requirement for Management Web Server

	Clean Installed Ubuntu 12.04 (or 13.04)
	apt-get

### Requirement for Physical(Compute) Node

	Clean Installed Ubuntu 12.04 (or 13.04)
	apt-get
	libvirt, screen, socat, kvm, nfs-common, openssh-server, libpam-krb5

### Guide for Memangement Node

* ./setup-mgm.sh
* Input mysql root's password
* Input DDNS Info
* Connect, http://{installed Server IP}
* Web-UI Administrator ID/PW: admin / 1234 (Must change admin's password)
* Add Primary/Secondary Storage (NFS Shared Storage Must be prepared first.)
* Add Template from "https://plink.ucloud.com/public_link/link/b9f32add350b3706", Name/Desc is "Template-Ubuntu_12.04.2_64.qcow2", etc is KVM, 64bit, Debian.
* Add Network-Pool Range: No Router, Direct IP to VM (e.g: 172.21.3.101 ~ 172.21.3.250)
* Add Physical Node(Compute Node) by password method.
* Test Create VM, and Enjoy.

### Guide for Physical Node

* Copy to Physical Node(Ubuntu13.04), then  Manual execute....
* Check script content.. changed "@_DNS_@" to "IP Address".

### NFS Server's /etc/exportfs Example

	/home/nfs/pri   *(rw,async,no_root_squash)
	/home/nfs/sec   *(rw,async,no_root_squash)

Next Step
=========

* Source code cleanup.
* Router per Tenant for Private-IPs.
* Live & On-Line Snapshot.
* VXLAN for Efficient traffic engineering and isolation.
* Load-Balancer with HAProxy.
* Stabilization: Life-Cycle, Scheduler, Multi-Tenant, Monitoring, and etc...

License and Author
==================

* Author: JungJungIn (<call518@gmail.com>)
* GNU GENERAL PUBLIC LICENSE Version 2
* Board/Member/Login System's Source from http://www.miwit.com and http://sir.co.kr
