---
layout: post
current: post
cover:  assets/built/images/programmers_logo.jpg
navigation: True
title: 프로그래머스 - 스킬트리(Queue, Stack)
date: 2021-11-08 16:40:00
tags: [programmers, queue, stack]
class: post-template
subclass: 'post tag-python'
author: sanghyoson
---
<i class="fa fa-search">&nbsp;</i> 
<a href='https://programmers.co.kr/learn/courses/30/lessons/42583'> Queue / Stack - 스킬트리</a>
![프로그래머스 사진](../assets/built/images/programmers_logo.jpg){: width="100%" height="100%"}

<h2>문제 설명</h2>
<br/>
선행 스킬이란 어떤 스킬을 배우기 전에 먼저 배워야 하는 스킬을 뜻합니다.

예를 들어 선행 스킬 순서가 스파크 → 라이트닝 볼트 → 썬더일때, 썬더를 배우려면 먼저 라이트닝 볼트를 배워야 하고, 라이트닝 볼트를 배우려면 먼저 스파크를 배워야 합니다.

위 순서에 없는 다른 스킬(힐링 등)은 순서에 상관없이 배울 수 있습니다. 따라서 스파크 → 힐링 → 라이트닝 볼트 → 썬더와 같은 스킬트리는 가능하지만, 썬더 → 스파크나 라이트닝 볼트 → 스파크 → 힐링 → 썬더와 같은 스킬트리는 불가능합니다.

선행 스킬 순서 skill과 유저들이 만든 스킬트리1를 담은 배열 skill_trees가 매개변수로 주어질 때, 가능한 스킬트리 개수를 return 하는 solution 함수를 작성해주세요.
<br/>
<br/>


<h2>제한 사항</h2>
<ul class = 'data-contents'>
<br/>
<li>스킬은 알파벳 대문자로 표기하며, 모든 문자열은 알파벳 대문자로만 이루어져 있습니다.</li>
<li>스킬 순서와 스킬트리는 문자열로 표기합니다.</li>
<li>예를 들어, C → B → D 라면 "CBD"로 표기합니다</li>
<li>선행 스킬 순서 skill의 길이는 1 이상 26 이하이며, 스킬은 중복해 주어지지 않습니다.</li>
<li>skill_trees는 길이 1 이상 20 이하인 배열입니다.</li>
<li>skill_trees의 원소는 스킬을 나타내는 문자열입니다.</li>
<li>skill_trees의 원소는 길이가 2 이상 26 이하인 문자열이며, 스킬이 중복해 주어지지 않습니다.</li>
</ul>
<br/>



<h2>입출력 예</h2>

| skill | skill_trees | return |
|---|---|---|
|'CBD'|['BACDE',    'CBADF','   AECB',  'BDA']|2|

<br/>


<!-- <h2>출력 형식</h2>
<ul class = 'data-contents'>
<br/>
<li>solution 함수에서는 로그 데이터 lines 배열에 대해 초당 최대 처리량을 리턴한다.</li>
</ul>
<br/> -->

<h2>문제 풀이</h2>
<br/>
Queue를 이용하여서 해결. 큰 접근 접근 방법은 Skill Trees에서 Skill에 속한 요소들만 남긴 후, 해당 값들의 순서를 확인하는 것이다. 
<br/>
<br/>


<h2>최종 코드</h2>
~~~python
from collections import deque as dq

def solution(skill, skill_trees):
    answer = 0
    for i, skill_tree in enumerate(skill_trees):
        for s in skill_tree:
            if s not in skill:
                skill_tree = skill_tree.replace(s, '')
        skill_trees[i] = skill_tree
        q = dq(skill_tree)
        sk = dq(skill)
        for i in range(len(skill_tree)):
            if q[0] == sk[0]:
                q.popleft()
                sk.popleft()
        if len(q) == 0:
            answer += 1
    return answer
~~~
<br/>
<h2>수정 코드</h2>
<br/>
위의 알고리즘으로 문제를 해결하긴 하였으나, 불필요하게 긴 것 같다.(못 짠거 같음 ...), 굳이 큐 / 스택을 사용하지 않고도 효율적이고, 가독성 좋은 코드라 남겨 놓음 ...
<br/>

~~~python
def solution(skill, skill_trees):
    answer = 0
    for skill_tree in skill_trees:
        sl = ''
        for c in skill_tree:
            if c in skill:
                sl += c
        
        if sl == skill[:len(sl)]:
            answer +=1
    return answer
~~~
