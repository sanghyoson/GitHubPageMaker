---
layout: post
current: post
cover:  assets/built/images/internet.jpg
navigation: True
title: 인터넷(3) - 브라우저와 작동 원리
date: 2021-11-04 12:40:00
tags: [roadmap, internet]
class: post-template
subclass: 'post tag-python'
author: sanghyoson
---
{% include backend-internet-table-of-contents.html %}
<br/>
![인터넷 사진](../assets/built/images/internet.jpg){: width="100%" height="100%"}

브라우저의 주요 기능은, '선택한 자원을 서버에게 요청하고, 전송받은 자원을 브라우저 화면에 표시'하는 것이다.
자원의 종류는 아래와 같은 요소들이 될 수 있다.

자원의 종류

HTML
CSS
JavaScript
PDF
Image
기타 등등

URI는 각 자원의 서버 주소를 말한다. 이 주소는 서버 어딘가에 명시되어 있고, 명시된 주소를 통해 서버에게 해당 주소의 자원을 요청하여 받아오게 된다.
URI를 통한 자원 요청 방법은 브라우저에 있는 주소입력 창이 될 수도 있고, 데이터 요청을 위한 API 주소가 될 수도 있다. 클라우드 서비스로 따지면 S3 버킷 안에 들어있는 이미지의 엔드포인트가 될 수도 있겠다.
















**HTTP**(HyperText Transfer Protocol)의 약어로서 웹 상에서 정보를 주고받을 수 있는 **프로토콜**이다. 텍스트 기반으로 이루어져 있으며 약속과 같은 통신 규약을 정하였기 때문에 이 규약에 맞추어 정보를 주고 받을 수 있게 된다.
HTTP는 **클라이언트**(Client)와 **서버**(Server) 사이에 이루어지는 요청과 응답을 위한 프로토콜이다. 웹에서 클라이언트인 웹 브라우저(Web Browser)가 HTTP를 통해 서버에게 웹페이지(HTML, 그림 정보) 등을 요청하면, 서버는 이 요청에 응답하여 필요한 정보를 해당 정보를 필요로하는 사용자에게 전달한다. 비유적으로 설명을 하면, 우리가 물건을 구매할 때 클라이언트와 서버는 각각 우리와 점원이라고 생각할 수 있으며, 이때 구매하는 물건을 HTML이라는 정보라고 볼 수 있다. 물건을 요청하고 요청에 대한 응답을 HTTP라고 생각하면 이해가 쉽다.
<br/>
<br/>

<h2>메시지 포맷</h2>
<br/>
HTTP는 ASCII 메시지로 이루어진다.
<h4>요청 메시지</h4>
<br/>
클라이언트가 서버에게 보내는 요청 메시지는 '요청 내용', '헤더', '빈줄', '기타 내용' 등을 포함한다.
요청 내용 종류는 다음과 같은 것들이 있다.

<ul class = 'data-contents'>
    <li>GET : 자료 요청</li>
    <li>POST : 자료 생성 요청</li>
    <li>PUT : 자료 수정 요청</li>
    <li>DELETE : 자료의 삭제 요청</li>
</ul>
<br/>
<h4>응답 메시지</h4>
<br/>
서버가 클라이언트에게 전송하는 메시지에는 '상태코드', '헤더', '빈줄', '기타 내용'을 포함한다.
요청 메시지와 달리 응답은 상태코드로 전송되며 상태 코드 종류는 다음과 같다.

<ul class = 'data-contents'>
    <li>1XX (정보) : 정보 교환, 일부 요청을 받았음을 의미</li>
    <li>2XX (성공) : 데이터 전송이 성공적이거나, 수락되었음을 의미</li>
    <li>3XX (Redirection) : 바료의 위치가 바뀌었음을 의미</li>
    <li>4XX (요청 오류) : 클라이언트 측 오류</li>
    <li>5XX (서버 오류) : 서버 측 오류</li>
</ul>
