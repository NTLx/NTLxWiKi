---
title: proxychains
description: 
published: true
date: 2020-02-27T01:42:02.200Z
tags: 
---

# Manjaro

## Install

```bash
yay -S proxychains-ng
```

## Setting

edit `/etc/proxychains.conf` , commented out `proxy_dns` , then add `socks5 127.0.0.1 10088` .

## Usage

```bash
proxychains axel https://ftp.ncbi.nih.gov/blast/db/nr.00.tar.gz
```