---
layout: post
title:  "Setting your Wi-Fi to 802.11n-only can make IoT devices stop working"
categories: tech
---

Setting your router's Wi-Fi to be exclusively 802.11n greenfield can make your wireless 'smart' devices stop working in mysterious ways, even if they claim to support 802.11b/g/n. Under this scenario, the device may be able to see the 802.11n-exclusive AP, but can never connect to it, or claims to be connected but never gets a valid IP.

This is a fairly obscure problem that you won't encounter unless you tinker with your router's Wi-Fi settings. The default configuration of routers is never N-only, because the performance benefit is negligible, while potential compatibility problems such as these are real. 

I encountered this situation with the FitBit Aria smart scale, which supports 802.11b only. I discovered that the scale was 802.11b-only after awhile of troubleshooting the FitBit Aria's setup process, as the scale successfully detects the AP and accepts the Wi-Fi password, but can never connect. The Wireless B detail was a bit of fine print in the specifications.

The Brother MFC-J875DW wireless multifunction printer claims to support 802.11b/g/n, but also chokes on an N-only network. It'll display the AP name and accept a valid password, then claim to successfully connect. Unfortunately, it never gets a valid IP address. The worst part is that it prints out a status page every time Wi-Fi is 'successfully' configured.
