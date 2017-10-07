---
title: Using Ansible to build a high availablity Sabnzbd usenet downloader  
date: 2017/10/08 20:46:25
tags:
  - sabnzbd
  - usenet
category:
  - linux
thumbnail: http://static1.squarespace.com/static/5441db9ae4b0ea3fd727c19f/5441e39fe4b0c5dff241f1e5/54433308e4b0ea3fd7299c85/1419957053419/?format=80w
---
I'm limited to about 40MB/s on downloads on my VPC at Digital Ocean, but I run (sabnzbd)[https://sabnzbd.org/] for downloading large files from usenet.  It doesn't take long to download at all, but out of curiosity I wanted to see if I could parallelize this and download multiple files at the same.  I use Sonarr for searching usenet for freely distributable training videos which then sends them to SABnzbd for downloading.  Since Sonarr can send multiple files to sabnzbd which get queued up, I figured I can reduce the queue by downloading them at the same time.

Using Ansible and Terraform (devops automation tools), I can spin up VPC on demand, provision them, configure them as sabnzbd download nodes and then destroy the instances when complete.

The instances all run the same sabnzbd config and the instances use haproxy for round-robin distribution.  I will probably change this to (Consul)[], but I just wanted something quick so I used a basic haproxy config.

This is the terraform script that builds X sabnzbd instances and 1 haproxy instance.  It configures a VIP which I point Sonarr to.

Here is the ansible playbook that configuress the instances.

[](image: images/tech/terraform.png)
