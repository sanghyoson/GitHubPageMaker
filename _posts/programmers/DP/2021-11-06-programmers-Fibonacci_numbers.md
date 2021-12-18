---
layout: post
current: post
cover:  assets/built/images/programmers_logo.jpg
navigation: True
title: 프로그래머스 - 피보나치 수(DP)
date: 2021-11-06 21:40:00
tags: [programmers, dp]
class: post-template
subclass: 'post tag-python'
author: sanghyoson
---
<i class="fa fa-search">&nbsp;</i> 
<a href='https://programmers.co.kr/learn/courses/30/lessons/42895'> Dynamic Programming - 피보나치 수</a>
![프로그래머스 사진](../assets/built/images/programmers_logo.jpg){: width="100%" height="100%"}

<h2>문제 설명</h2>
<br/>
피보나치 수는 F(0) = 0, F(1) = 1일 때, 1 이상의 n에 대하여 F(n) = F(n-1) + F(n-2) 가 적용되는 수 입니다.
<ul class = 'data-contents'>
<li>F(2) = F(0) + F(1) = 0 + 1 = 1</li>
<li>F(3) = F(1) + F(2) = 1 + 1 = 2</li>
<li>F(4) = F(2) + F(3) = 1 + 2 = 3</li>
<li>F(5) = F(3) + F(4) = 2 + 3 = 5</li>
</ul>
와 같이 이어집니다.
2 이상의 n이 입력되었을 때, n번째 피보나치 수를 1234567으로 나눈 나머지를 리턴하는 함수, solution을 완성해 주세요.
<br/>
<br/>


<h2>제한 사항</h2>
<ul class = 'data-contents'>
<br/>
<li>n은 2 이상 100,000 이하인 자연수입니다.</li>
</ul>
<br/>

<!-- <h2>출력 형식</h2>
<ul class = 'data-contents'>
<br/>
<li>solution 함수에서는 로그 데이터 lines 배열에 대해 초당 최대 처리량을 리턴한다.</li>
</ul>
<br/> -->

<h2>문제 풀이</h2>
<br/>
DP를 이용해서 접근했다. 단순하게 반복문을 이용해서 구할 경우, 불필요하게 반복되는 과정이 많아진다. 예로들어, F(5)를 구한다고 하면, F(5) = F(4) + F(3)를 이용해서 값을 연산한다. F(4) = F(3) + F(2)이며, F(2) = F(1) + F(0)이다. 한편 F(4)를 연산 후 F(3)을 연산해야 F(5)를 구할 수 있는데, 앞서 진행한 과정을 보면 F(4)를 연산하는 과정에서 F(3)을 연산했음에도 불구하고 F(3)을 구하는 과정을 반복한다. 이와 같이 이미 처리한 과정을 반복하는 것을 방지하기 위해서 이미 연산한 것을 저장하는 DP를 이용하였다.
<br/>
<br/>



<h2>최종 코드</h2>
~~~python
def solution(n):
    dic = {0 : 0, 1 : 1}
    
    for i in range(n+1):
        if not i in dic:
            dic[i] = dic[i-1] + dic[i-2]
    
    answer = dic[n]%1234567
    return answer
~~~
