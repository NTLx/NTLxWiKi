---
title: Git
description: 
published: true
date: 2020-05-07T08:32:26.093Z
tags: 
---

# Using proxy

```bash
ssh-keygen -t rsa -b 4096 -C "lx3325360@gmail.com"
git config --global user.name "NTLx"
git config --global user.email "lx3325360@gmail.com"
git config --global http.proxy http://127.0.0.1:8888
git config --global https.proxy http://127.0.0.1:8888
```