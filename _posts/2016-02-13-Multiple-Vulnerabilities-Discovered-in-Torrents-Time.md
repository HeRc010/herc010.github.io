---
layout: post
category: vulnerabilities and exploits
title: "Multiple Vulnerabilities Discovered in the Torrents Time Application"
tagline: ""
tags : [vulnerability, exploit, Torrents Time]
---
{% include JB/setup %}

## TL;DR

A significant number of vulnerabilities in the Torents Time application were recently discovered [1].

## Overview

Torrents Time (hereafter abbreviated as TT) is an application which facilitates the ‘instant’ download and streaming of torrented material within a browser, as an alternative to downloading the torrent using a local torrent client. TT is currently experiencing widespread use after adoption by multiple popular torrenting websites, including The Pirate Bay, as a streaming feature [2].

## Installation Details

Users of TT are required to download an installer, which deploys a local node.js server and installs a browser plugin.

## CORS Abuse

TT is subject to MITM attacks due to the improper implementation of CORS requests. As a result, a web page which mimics the web page being accessed by a user may be fabricated by an attacker with an additional script in the HTML head tag. The attacker may subsequently make use of the functionality loaded in the TT scripts. Possible malicious activities include:

Issuing a torrent which was not originally requested by the user
Introducing malicious code into the downloaded content
Acquisition of information by those interested (advertisers for example) which can be used to track users online

## Root Access on Mac OS X

The OS X TT client runs with root access, rendering Apple users immensely vulnerable to a wide range of malicious activities.

## Browser Plugin Installer Download

The plugin installer may be programmatically re-downloaded, however after minor changes an alternate executable may be downloaded instead, affording an attacker the opportunity for any number of malicious activities, including but not limited to the installation of malware.

## Sources

[1] [blog.andrew.im, "Torrents-time Security Issues", 2016.](http://blog.andrew.im/post/139084882590/torrents-time-security-issues) [Accessed: 13-Feb-2016].  
[2] [news.softpedia.com, "Torrents Time Plugin Plagued by Security Issues, Pirate Bay & KAT Users at Risk", 2016.](http://news.softpedia.com/news/torrents-time-plugin-plagued-by-security-issues-pirate-bay-kat-users-at-risk-500334.shtml) [Accessed: 13-Feb-2016].

Enter text in [Markdown](http://daringfireball.net/projects/markdown/). Use the toolbar above, or click the **?** button for formatting help.
