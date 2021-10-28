---
layout: post
current: post
cover:  assets/built/images/internet.jpg
navigation: True
title: 인터넷(2) - HTTP는 무엇인가?
date: 2021-10-12 12:40:00
tags: [roadmap, internet]
class: post-template
subclass: 'post tag-python'
author: sanghyoson
---
{% include backend-internet-table-of-contents.html %}
<br/>
![인터넷 사진](../assets/built/images/internet.jpg){: width="100%" height="100%"}

**인터넷**(Internet)이란 International Network의 줄임말로 Web의 가장 핵심적인 기술이라고 할 수 있다.
기본적으로, 인터넷이란 무수히 많은 컴퓨터들이 통신할 수 있도록 하는 **거대한 네트워크 통신망**이다.
수많은 컴퓨터들이 통신하기 위해서 컴퓨터 **TCP/IP**를 이용하는데 이 장에서는 인터넷이 기본적으로 어떻게 작동하는지만 다룬다.

<h3>두 대의 컴퓨터로 이루어진 단순한 네트워크</h3>
![2대 컴퓨터](../assets/built/images/internet_network_1_one2one.jpg){: width="50%" height="50%"}
인터넷이라는 커다란 네트워크를 이해하기 전 아주 작은 네트워크에 대해서 먼저 이해를 하자.
서로 다른 두 대의 컴퓨터가 통신을 하기위해서는 서로의 컴퓨터가 물리적(Ethernet) 혹은 무선(WiFi, Bluetooth)으로 **연결**되어 있어야 한다.
