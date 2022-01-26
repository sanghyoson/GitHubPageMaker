---
layout: post
current: post
cover:  assets/built/images/programmers_logo.jpg
navigation: True
title: 프로그래머스 - 괄호 회전하기(Queue, Stack)
date: 2021-11-06 14:40:00
tags: [programmers, queue, stack]
class: post-template
subclass: 'post tag-python'
author: sanghyoson
---
<i class="fa fa-search">&nbsp;</i> 
<a href='https://programmers.co.kr/learn/courses/30/lessons/76502'> Queue / Stack - 괄호 회전하기</a>
![프로그래머스 사진](../assets/built/images/programmers_logo.jpg){: width="100%" height="100%"}

<h2>문제 설명</h2>
<br/>
다음 규칙을 지키는 문자열을 올바른 괄호 문자열이라고 정의합니다.
<ul class = 'data-contents'>
<li>(), [], {} 는 모두 올바른 괄호 문자열입니다.</li>
<li>만약 A가 올바른 괄호 문자열이라면, (A), [A], {A} 도 올바른 괄호 문자열입니다. 예를 들어, [] 가 올바른 괄호 문자열이므로, ([]) 도 올바른 괄호 문자열입니다.</li>
<li>만약 A, B가 올바른 괄호 문자열이라면, AB 도 올바른 괄호 문자열입니다. 예를 들어, {} 와 ([]) 가 올바른 괄호 문자열이므로, {}([]) 도 올바른 괄호 문자열입니다.</li>
</ul>
대괄호, 중괄호, 그리고 소괄호로 이루어진 문자열 s가 매개변수로 주어집니다. 이 s를 왼쪽으로 x (0 ≤ x < (s의 길이)) 칸만큼 회전시켰을 때 s가 올바른 괄호 문자열이 되게 하는 x의 개수를 return 하도록 solution 함수를 완성해주세요.
<br/>
<br/>

<h2>제한 사항</h2>
<ul class = 'data-contents'>
<br/>
<li>s의 길이는 1 이상 1,000 이하입니다.</li>
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
<a href='https://programmers.co.kr/learn/courses/30/lessons/12909'>올바른 괄호</a> 문제의 확장이라고 보면 되기에 기본적인 접근 방법도 동일하다. 스택과 큐를 이용하였다. 스택에 괄호들을 쌓고 올바른 순서대로 들어왔을 경우 빈스택이 되도록 하는 것이다. 추가적으로 문자열을 문자열의 길이만큼 회전시키는 코드만 추가하였다. 리스트 슬라이싱을 이용해서 i번째까지의 리스트를 남은 리스트의 뒤쪽에 이어붙이는 방식으로 새로운 리스트를 생성하였다.
~~~python
    cnt = 0
    for i in range(len(s)):
        sl = list(s)
        sl = sl[i:] + sl[:i]
        st = ''.join(sl)
        if checkRight(st):
            cnt += 1
    return cnt
~~~


<br/>


<h2>최종 코드</h2>
~~~python
from collections import deque as dq

def solution(s):
from collections import deque as dq

def checkRight(s):
    queue = dq(s)
    stack = []
    while queue:
        pop = queue.popleft()
        if len(stack) == 0:
            stack.append(pop)
        else:
            if pop == '}' and stack[-1] == '{':
                stack.pop()
            elif pop == ']' and stack[-1] == '[':
                stack.pop()
            elif pop == ')' and stack[-1] == '(':
                stack.pop()
            else:
                stack.append(pop)
    return True if len(stack) == 0 else False

def solution(s):
    cnt = 0
    for i in range(len(s)):
        sl = list(s)
        sl = sl[i:] + sl[:i]
        st = ''.join(sl)
        if checkRight(st):
            cnt += 1
    return cnt
~~~
