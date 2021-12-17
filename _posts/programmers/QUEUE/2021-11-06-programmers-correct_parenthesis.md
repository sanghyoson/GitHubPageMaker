---
layout: post
current: post
cover:  assets/built/images/programmers_logo.jpg
navigation: True
title: 프로그래머스 - 올바른 괄호(Queue, Stack)
date: 2021-11-06 13:40:00
tags: [programmers, queue, stack]
class: post-template
subclass: 'post tag-python'
author: sanghyoson
---
<i class="fa fa-search">&nbsp;</i> 
<a href='https://programmers.co.kr/learn/courses/30/lessons/12909'> Queue / Stack - 올바른 괄호</a>
![프로그래머스 사진](../assets/built/images/programmers_logo.jpg){: width="100%" height="100%"}

<h2>문제 설명</h2>
<br/>
괄호가 바르게 짝지어졌다는 것은 '(' 문자로 열렸으면 반드시 짝지어서 ')' 문자로 닫혀야 한다는 뜻입니다. 예를 들어
<ul class = 'data-contents'>
<li>"()()" 또는 "(())()" 는 올바른 괄호입니다.</li>
<li>")()(" 또는 "(()(" 는 올바르지 않은 괄호입니다.</li>
</ul>
'(' 또는 ')' 로만 이루어진 문자열 s가 주어졌을 때, 문자열 s가 올바른 괄호이면 true를 return 하고, 올바르지 않은 괄호이면 false를 return 하는 solution 함수를 완성해 주세요.
<br/>
<br/>

<h2>제한 사항</h2>
<ul class = 'data-contents'>
<br/>
<li>문자열 s의 길이 : 100,000 이하의 자연수</li>
<li>문자열 s는 '(' 또는 ')' 로만 이루어져 있습니다.</li>
</ul>
<br/>

<!-- <h2>출력 형식</h2>
<ul class = 'data-contents'>
<br/>
<li>solution 함수에서는 로그 데이터 lines 배열에 대해 초당 최대 처리량을 리턴한다.</li>
</ul>
<br/> -->

<h2>풀이과정</h2>
<br/>
스택과 큐를 이용하여 접근하였다. 아이디어는 다음과 같다. 빈 스택에 입력으로 받은 괄호 문자열을 순차적으로 받았을 때, 스택에 쌓인 전후 쌍을 이루면 스택에서 제거한다. 예로 ['(', ')']과 같은 쌍을 이룬다면, [] 쌍을 비우는 방법이다. 해당 방법대로 진행을 하면, 올바른 문자열인 경우 최종적으로 빈 스택만 남게된다.

<br/>


<h2>최종 코드</h2>
~~~python
from collections import deque as dq

def solution(s):
    queue = dq(s)
    stack = []
    
    while queue:
        pop = queue.popleft()
        if len(stack) == 0:
            stack.append(pop)
        else:
            if stack[-1] == '(' and pop == ')':
                stack.pop()
            else:
                stack.append(pop)
    return True if len(stack)==0 else False
~~~
