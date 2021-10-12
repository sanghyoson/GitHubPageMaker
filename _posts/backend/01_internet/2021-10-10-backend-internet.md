---
layout: post
current: post
cover:  assets/built/images/jekyll-logo.png
navigation: True
title: 인터넷(1) - 인터넷은 어떻게 작동하는가?
date: 2021-10-10 16:40:00
tags: [backend, internet]
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

<h3>N 대의 컴퓨터로 이루어진 단순한 네트워크</h3>
![N대 컴퓨터](../assets/built/images/internet_network_2_multi2multi.jpg){: width="50%" height="50%"}
두 대만의 컴퓨터로는 하나의 유선 케이블(무선도 동일)이 필요하다. 
네트워크는 이렇게 간단하지 않으므로 N 대의 컴퓨터를 고려하자.
각각의 컴퓨터를 모두 연결하려면 필요한 유선 케이블 수는 **<sub>N</sub>C<sub>2</sub>**개이다. 
단순하게 컴퓨터를 연결하는 방법으로는 인터넷이라는 거대한 네트워크를 구축하기에는 제약이 있다.

<h3>라우터을 이용한 단순한 네트워크</h3>
![라우터 연결](../assets/built/images/internet_network_3_router.jpg){: width="50%" height="50%"}
직접적으로 연결하는 문제를 해결하기 위해 **라우터**(Router)라는 소형 컴퓨터를 사용한다.
여러대의 컴퓨터는 직접적으로 연결하는 것이 라우터에 연결된다.
라우터는 중간 전달자 역할을 하는데, 각 컴퓨터가 보내려고 하는 데이터를 받아 보내려는 컴퓨터로 정확하게 전달한다.

> 사전적 의미의 라우터(Router)란 네트워크와 네트워크 간의 경로를 설정하고 빠른 길로 트래픽을 이끌어주는 장비.
> 대표적인 기능은 네트워크 간의 연결이지만, NAT(Network Address Translation), 방화벽, VPN 등 부가 기능도 함께 제공한다. 

![라우터 확장](../assets/built/images/internet_network_4_router_expand.jpg){: width="50%" height="50%"}
컴퓨터를 확장하였듯 라우터도 확장이 가능하다.
라우터를 확장하게 되면 앞서 언급한 네트워크들보다 훨씬 큰 네트워크를 구축할 수 있다.
하지만, 라우터도 역시 한계는 존재한다. 
우리의 목적을 위해 네트워크를 구축하였듯 다른 사람들도 다른 지역에서 라우터를 이용하여 새로운 네트워크를 구축할 수 있다.
하지만 유선 케이블(무선 통신도 동일)을 먼 곳까지 모두 연결하는 것은 불가능하다.
![모뎀 연결](../assets/built/images/internet_network_5_modem.jpg){: width="60%" height="60%"}
이를 가능하도록 하는 무엇인가가 필요한데, 이미 구축하여 세계 여러 지역에서 사용하고 있는 전화라는 좋은 시스템을 이용할 수 있다.
따라서, 이미 구축되어 있는 전화 시스템과 라우터를 이용하여 구축한 네트워크를 연결할 수 있는 **모뎀**이라는 장비를 이용한다.
모뎀을 통해서 인터넷 서비스 제공 업체(Internet Service Provider, **ISP**)에 접근할 수 있고, ISP가 구축한 네트워크를 통해 접근하려는 대상 네트워크로 접근이 가능하게 된다.
이러한 전체적인 네트워크 인프라로 인터넷은 구성된다.
![인터넷 통신 네트워크](../assets/built/images/internet_network_6_internet.jpg){: width="200 %" height="200%"}
