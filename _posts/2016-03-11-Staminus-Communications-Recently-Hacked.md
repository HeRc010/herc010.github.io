---
layout: post
category: vulnerabilities and exploits
title: "Staminus Communications Recently Hacked"
tagline: ""
tags : [vulnerability, exploit, Staminus Communications]
---
{% include JB/setup %}

## TL;DR

Staminus Communications was recently compromised, resulting in the collapse of the company network and the leakage of large volumes of sensitive information, including credit card information [1].

## Overview

Staminus Communications provides services which are intended to mitigate (or eliminate entirely) the effects of DDoS attacks. One such service provided by Staminus Communications is ‘Intreppid’ which provides virtual private servers, along with added features to facilitate DDoS protection.

An unknown hacker group subverted the server backbone of Staminus Communications and, after reverting the servers to factory settings, caused the collapse of Staminus’ network.

The contents of multiple databases (Staminus’ main database, the Intreppid database and the database of a Staminus’ client) were leaked using a Hastebin link, which contained Tor links to files stolen from the databases.

Additionally, the Hastebin link contained a satirical list of ‘Tips when Running a Security Company’ which disclosed potential vulnerabilities which were likely exploited during the attack [2], including but not limited to a shared root password used by the servers, exposed power distribution units on a telnet WAN and comprehensive credit card information being stored in plaintext.

##Sources

[1] [news.softpedia.com, "Hackers Breach DDoS Protection Firm Staminus", 2016.](http://news.softpedia.com/news/hackers-breach-ddos-protection-firm-staminus-501625.shtml) [Accessed: 11-Mar-2016].
[2] [reddit.com, "Staminus Communications and KKK.com Hacked in Major Security Breach", 2016.](http://news.softpedia.com/news/hackers-breach-ddos-protection-firm-staminus-501625.shtml) [Accessed: 11-Mar-2016].