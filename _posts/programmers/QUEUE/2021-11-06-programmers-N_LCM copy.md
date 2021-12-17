---
layout: post
current: post
cover:  assets/built/images/programmers_logo.jpg
navigation: True
title: 프로그래머스 - N개의 최소 공배수(Queue, Stack)
date: 2021-11-06 12:40:00
tags: [programmers, queue, stack]
class: post-template
subclass: 'post tag-python'
author: sanghyoson
---
<i class="fa fa-search">&nbsp;</i> 
<a href='https://programmers.co.kr/learn/courses/30/lessons/12953'> Queue / Stack - N개의 최소 공배수</a>
![프로그래머스 사진](../assets/built/images/programmers_logo.jpg){: width="100%" height="100%"}

<h2>문제 설명</h2>
<br/>
두 수의 최소공배수(Least Common Multiple)란 입력된 두 수의 배수 중 공통이 되는 가장 작은 숫자를 의미합니다. 예를 들어 2와 7의 최소공배수는 14가 됩니다. 정의를 확장해서, n개의 수의 최소공배수는 n 개의 수들의 배수 중 공통이 되는 가장 작은 숫자가 됩니다. n개의 숫자를 담은 배열 arr이 입력되었을 때 이 수들의 최소공배수를 반환하는 함수, solution을 완성해 주세요.

<br/>

<h2>제한 사항</h2>
<ul class = 'data-contents'>
<br/>
<li>arr은 길이 1이상, 15이하인 배열입니다.</li>
<li>arr의 원소는 100 이하인 자연수입니다.</li>
</ul>
<br/>

<!-- <h2>출력 형식</h2>
<ul class = 'data-contents'>
<br/>
<li>solution 함수에서는 로그 데이터 lines 배열에 대해 초당 최대 처리량을 리턴한다.</li>
</ul>
<br/> 

<h2>문제 풀이</h2>
<br/>
N을 최소한으로 이용하여 number를 구해야 하는데, **동일한 개수의 N을 가지고 표현할 수 있는 수는 매우 많다**. 접근방법은 N의 개수를 늘려가며 표현할 수 있는 수를 빈틈없이 계산하고 이 값들 중에서 number가 포함되는지 확인하는 것이다.
<ol class = 'data-contents'>
    <li>1. n개의 N을 이용하여 구할 수 있는 수 나열</li>
    <li>2. 나열된 수 중 number가 존재하는 확인</li>
</ol>
<br/>
-->

<h2>풀이과정</h2>
<br/>
두 수의 최소 공배수(Least Common Multiple, **LCM**)를 구하는 방법은 두 수의 곱을 최대 공약수(Greatest Common Divisor)로 나눈 것과 같다. N개의 최소 공배수를 구하는 접근 방법은 다음과 같다.
> a<sub>1</sub>, a<sub>2</sub>, a<sub>3</sub>,  .... a<sub>N</sub> : N 개의 수

<ol class = 'data-contents'>
    <li>1. a<sub>1</sub>, a<sub>2</sub>의 LCM인 a<sup>`</sup><sub>1</sub>를 구한다.</li>
    <li>2. a<sup>`</sup><sub>1</sub>과 a<sub>3</sub>의 LCM인 a<sup>`</sup><sub>2</sub>를 구한다.</li>
    <li>3. a<sup>`</sup><sub>m</sub>인 하나의 수가 남도록 위를 반복한다.</li>
</ol>
<br/>


<h2>최종 코드</h2>
~~~python
from collections import deque as dq

def gcd(a, b):
    while b > 0:
        a, b = b, a%b
    return a

def solution(arr):
    queue = dq(arr)
    result = queue.popleft()
    while queue:
        a = queue.popleft()
        result = result*a/gcd(a, result)
    return result
~~~
