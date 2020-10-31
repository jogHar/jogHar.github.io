---
layout: post
title:  "'You are not the owner' when copy other user file in Ubuntu"
date:   2020-10-31 08:38:11 +0530
categories: []
tags: ubuntu
author: "Hardik Jogani"
---

## 1. Copy file/folder from other user in Ubuntu.
- copy file one user to another user
``` terminal
sudo cp /home/user1/path /home/user2/path
```
- using above command you copy file successfully but you can't access file because you are not owner of this file/folder.

## 2. Change owner of file/folder
- 
``` terminal
sudo chown -R username /path/to/directory
```
- You must have sudo privileges though!
You should use -R option to operate on files and directories recursively
