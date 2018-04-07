---
layout: post
title:      "IP AVIAN CARRIES"
date:       2018-04-07 17:18:11 +0000
permalink:  ip_avian_carries
---

![](http://i.dailymail.co.uk/i/pix/2013/05/30/article-0-1A109382000005DC-956_634x432.jpg)

An example of poor latency.


As time has inched forward, the Sinatra project looms up ahead, challenging me to systematically combine the knowledge of the preceeding lessons into functional, ideally pretty, gestalt. I am more confident approaching the Sinatra portfolio project than I was approaching the Ruby gem. The form of the project and how the pieces fit together is more transparent. The thoughtful architecture of Flatiron's lessons has knowledge utilized again and again. We build on the past and what we have been building -- except for HTML/CSS, but more on that later. 

In delving the gradient lessons of the Sinatra project, I recently went down a TCP/IP hole. It struck me somewhat off-guard, as the only internet I've ever known is well evolved from the origins of it. I was particularly interested in the April Fool's experimental method of using *homing pigeons to carry internet protocol traffic*. To think experimental internet protocol traffic could be palpable and tangibly visible. Here's a 1990 memo from **Network Working Group**: [https://tools.ietf.org/html/rfc1149](http://). Take note of the section of the header stating this is an experimental method and that *errata exist*.

And then, in 2001, it was successfully implemented! Nine packets were sent, each with one ping. However, the testers only received four responses. Poor latency, abyssmal packet loss (55% packet loss).

```
Script started on Sat Apr 28 11:24:09 2001
$ /sbin/ifconfig tun0
tun0      Link encap:Point-to-Point Protocol
          inet addr:10.0.3.2  P-t-P:10.0.3.1  Mask:255.255.255.255
          UP POINTOPOINT RUNNING NOARP MULTICAST  MTU:150  Metric:1
          RX packets:1 errors:0 dropped:0 overruns:0 frame:0
          TX packets:2 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0
          RX bytes:88 (88.0 b)  TX bytes:168 (168.0 b)

$ ping -c 9 -i 900 10.0.3.1
PING 10.0.3.1 (10.0.3.1): 56 data bytes
64 bytes from 10.0.3.1: icmp_seq=0 ttl=255 time=6165731.1 ms
64 bytes from 10.0.3.1: icmp_seq=4 ttl=255 time=3211900.8 ms
64 bytes from 10.0.3.1: icmp_seq=2 ttl=255 time=5124922.8 ms
64 bytes from 10.0.3.1: icmp_seq=1 ttl=255 time=6388671.9 ms

--- 10.0.3.1 ping statistics ---
9 packets transmitted, 4 packets received, 55% packet loss
round-trip min/avg/max = 3211900.8/5222806.6/6388671.9 ms


Script done on Sat Apr 28 14:14:28 2001
```

I was inspired to learn about early TCP/IP creation and development when I was learning about using Rack. Namely, how is information sent and received over thousands of miles? But, the blog post, "How the Internet Works" will come much later.

Here are some links to TCP/IP information for a more 'rounded' understanding:
[Avian Carries](https://en.wikipedia.org/wiki/IP_over_Avian_Carriers) [and](https://tools.ietf.org/html/rfc1149)
[TCP/IP](https://en.wikipedia.org/wiki/Internet_protocol_suite)
[Network Architecture](https://tools.ietf.org/html/rfc1122)
