---
layout: post
current: post
cover:  assets/built/images/programmers_logo.jpg
navigation: True
title: 프로그래머스 - 프린터(Queue, Stack)
date: 2022-01-03 16:40:00
tags: [programmers, queue, stack]
class: post-template
subclass: 'post tag-python'
author: sanghyoson
---
<i class="fa fa-search">&nbsp;</i> 
<a href='https://programmers.co.kr/learn/courses/30/lessons/42583'> Queue / Stack - 프린터</a>
![프로그래머스 사진](../assets/built/images/programmers_logo.jpg){: width="100%" height="100%"}

<h2>문제 설명</h2>
<br/>
일반적인 프린터는 인쇄 요청이 들어온 순서대로 인쇄합니다. 그렇기 때문에 중요한 문서가 나중에 인쇄될 수 있습니다. 이런 문제를 보완하기 위해 중요도가 높은 문서를 먼저 인쇄하는 프린터를 개발했습니다. 이 새롭게 개발한 프린터는 아래와 같은 방식으로 인쇄 작업을 수행합니다.
<ul class = 'data-contents'>
<br/>
<li>1. 인쇄 대기목록의 가장 앞에 있는 문서(J)를 대기목록에서 꺼냅니다.</li>
<li>2. 나머지 인쇄 대기목록에서 J보다 중요도가 높은 문서가 한 개라도 존재하면 J를 대기목록의 가장 마지막에 넣습니다.</li>
<li>3. 그렇지 않으면 J를 인쇄합니다.</li>
</ul>

예를 들어, 4개의 문서(A, B, C, D)가 순서대로 인쇄 대기목록에 있고 중요도가 2 1 3 2 라면 C D A B 순으로 인쇄하게 됩니다.

내가 인쇄를 요청한 문서가 몇 번째로 인쇄되는지 알고 싶습니다. 위의 예에서 C는 1번째로, A는 3번째로 인쇄됩니다.

현재 대기목록에 있는 문서의 중요도가 순서대로 담긴 배열 priorities와 내가 인쇄를 요청한 문서가 현재 대기목록의 어떤 위치에 있는지를 알려주는 location이 매개변수로 주어질 때, 내가 인쇄를 요청한 문서가 몇 번째로 인쇄되는지 return 하도록 solution 함수를 작성해주세요.
<br/>
<br/>


<h2>제한 사항</h2>
<ul class = 'data-contents'>
<br/>
<li>현재 대기목록에는 1개 이상 100개 이하의 문서가 있습니다.</li>
<li>인쇄 작업의 중요도는 1~9로 표현하며 숫자가 클수록 중요하다는 뜻입니다.</li>
<li>location은 0 이상 (현재 대기목록에 있는 작업 수 - 1) 이하의 값을 가지며 대기목록의 가장 앞에 있으면 0, 두 번째에 있으면 1로 표현합니다.</li>
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
collections등의 모듈을 사용하지 않고 코드를 짜는 연습 중. 큐를 통해서 우선순위를 비교하고 해당 우선순위가 낮으면 다시 append한다.
<br/>
<br/>


<h2>최종 코드</h2>
~~~python
def solution(priorities, location):
    # queue 클래스 생성
    q = Queue();
    
    # 우선순우 포함한 큐 배열 생성
    for i in range(len(priorities)):
        q.eq([priorities[i], i])
        
    cnt = 0
    while q.queue:  
        pri, idx = q.dq();
        
        if q.queue:
            if pri >= max(list(zip(*q.queue))[0]):
                cnt += 1
                if idx == location:
                    return cnt
            else:
                q.eq([pri, idx])
        else:
            return cnt+1
        
class Queue:
    def __init__(self):
        self.queue = []

    def isEmpty(self):
        if not self.queue:
            return True
        else:
            return False

    def eq(self, data):
        self.queue.append(data)

    def dq(self):
        if self.isEmpty():
            return "Queue is Empty"
        else:
            dequeued = self.queue[0]
            self.queue = self.queue[1:]
            return dequeued

    # front가 무엇인지만 보여준다.
    def peek(self):
        if self.isEmpty():
            return "Queue is Empty"
        else:
            peeked = self.queue[0]
            return peeked
~~~