---
layout: post
title: Amazon Security Policy Compliance Audit
date: 2018-01-16 09-35-47
categories: blog
---

# Amazon Security Policy Compliance Audit

## NSW
- Host: dxfcgcnsw.toll.com.au
- Model: qemu-kvm, ver: 0.12.1.2, rel: 2.355.el6, arch: x86_64
```
  ssh dxfcgcnsw-host
  yum search qemu
  yum info qemu-kvm
  rpm -qa | grep -i kvm
```
- How to identify if it's a VM
```
  lshw -class system (recommend)
  cat /proc/cpuinfo
  virt-what
  dmidecode
  lshw
  dmesg | grep -i hypervisor
  cat /proc/meminfo | grep MemTotal | awk '{print $2/1024/1024}'
  awk '/MemTotal/ {print $2/1024/1024}' /proc/meminfo
  lshw -class disk -short | grep size
  fdisk -l
  lsb_release -a
  cat /proc/version
  http://opswiki.toll.com.au/wiki/index.php/Host:dxfcgcnsw-host
  http://fastfmspr01.toll.com.au/dokuwiki/doku.php?id=rockhopper:virtualisation:admin:host_matrix
  lscpu
  cat /proc/cpuinfo | grep "physical id" | sort -u | wc -l
  egrep -e "core id" -e ^physical /proc/cpuinfo|xargs -l2 echo|sort -u
  dmidecode | grep -i product
```
- [Virtual host matrix](http://fastfmspr01.toll.com.au/dokuwiki/doku.php?id=rockhopper:virtualisation:admin:host_matrix)

|	| Location	| Crystal Reports | Rockhopper guest	| despatchEXPRESS guest	| Comments |
|--:|----------:|----------------:|--------------------:|----------------------:|----------:|
|dxfcmmvic-host|VIC|tfaapaup005|dxfcmmvic|demel|tfaapaup005 - replaced APS6, demel switched off, not in use|
|dxfcgcnsw-host|NSW|tfaapaup002|dxfcgcnsw|desyd|tfaapaup002 - replaced APS2|
|tfavhaup001|QLD|tfaapaup004|dxfcmmqld|tfavhaup004 - replaced APS4.|
|tfavhaup002|WA|tfaapaup006|dxfcmmwa|tfaapaup006 - replaced APS5. (Initial VM built as fasapbelp1, by vitualising APS5.  Since replaced by tfaapaup006, which was built using a standard Windows VM image.)|
|tfavhaup003|SA|tfaapaup001|dxfctssa|tfaapaup001 - replaced APS3.|
|tfavhaup004|ACT|tfaapaup003|rhcan|tfaapaup002 - replaced APS8.|
|tfavhauu001|VIC|UAT - not configured.|

- [Virtualization host configuration and guest installation](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html-single/virtualization_host_configuration_and_guest_installation_guide/index)
- [Figuring out CPUs and Sockets](https://access.redhat.com/discussions/480953)
