---
layout: post
current: post
cover:  assets/built/images/programmers_logo.jpg
navigation: True
title: 프로그래머스 - 다리를 지나는 트럭(Queue, Stack)
date: 2021-11-07 16:40:00
tags: [programmers, queue, stack]
class: post-template
subclass: 'post tag-python'
author: sanghyoson
---
<i class="fa fa-search">&nbsp;</i> 
<a href='https://programmers.co.kr/learn/courses/30/lessons/42583'> Queue / Stack - 다리를 지나는 트럭</a>
![프로그래머스 사진](../assets/built/images/programmers_logo.jpg){: width="100%" height="100%"}

<h2>문제 설명</h2>
<br/>
트럭 여러 대가 강을 가로지르는 일차선 다리를 정해진 순으로 건너려 합니다. 모든 트럭이 다리를 건너려면 최소 몇 초가 걸리는지 알아내야 합니다. 다리에는 트럭이 최대 bridge_length대 올라갈 수 있으며, 다리는 weight 이하까지의 무게를 견딜 수 있습니다. 단, 다리에 완전히 오르지 않은 트럭의 무게는 무시합니다.

예를 들어, 트럭 2대가 올라갈 수 있고 무게를 10kg까지 견디는 다리가 있습니다. 무게가 [7, 4, 5, 6]kg인 트럭이 순서대로 최단 시간 안에 다리를 건너려면 다음과 같이 건너야 합니다.

|경과 시간|다리를 지난 트럭|다리를 건너는 트럭|대기 트럭|
|---|---|---|---|
|0|[]|[]|[7,4,5,6]|
|1~2|[]|[7]|[4,5,6]|
|3|	[7]|	[4]|	[5,6]|
|4	|[7]	|[4,5]	|[6]|
|5	|[7,4]|	[5]	|[6]|
|6~7	|[7,4,5]|	[6]	|[]|
|8	|[7,4,5,6]	|[]	|[]|

따라서, 모든 트럭이 다리를 지나려면 최소 8초가 걸립니다.

solution 함수의 매개변수로 다리에 올라갈 수 있는 트럭 수 bridge_length, 다리가 견딜 수 있는 무게 weight, 트럭 별 무게 truck_weights가 주어집니다. 이때 모든 트럭이 다리를 건너려면 최소 몇 초가 걸리는지 return 하도록 solution 함수를 완성하세요.
<br/>
<br/>


<h2>제한 사항</h2>
<ul class = 'data-contents'>
<br/>
<li>bridge_length는 1 이상 10,000 이하입니다.</li>
<li>weight는 1 이상 10,000 이하입니다.</li>
<li>truck_weights의 길이는 1 이상 10,000 이하입니다.</li>
<li>w모든 트럭의 무게는 1 이상 weight 이하입니다.</li>
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
Queue를 이용하여서 해결하였다. 다리 길이 크기를 갖는 큐를 생성하고, truck_weights에서 하나씩 큐로 이동하였다. 큐의 총 합이 최대 하중이 넘지 않을때만 truck_weights에서 옮기도록하였고, 각 시간 스텝마다 큐는 하나씩 왼쪽으로 이동시킨다. 최종적으로 큐 위의 모든 하중이 없고, truck_weights 리스트에 남은 원소가 존재하지 않았을 때의 시간을 구한다.
> 한편, sum() 함수를 이용하면, 많은 시간을 잡아 먹는다. sum()의 시간복잡도 O(N)
<br/>
<br/>


<h2>최종 코드</h2>
~~~python
from collections import deque as dq

def solution(bridge_length, weight, truck_weights):
    time = 0
    q = dq([0 for i in range(bridge_length)])
    suma = 0
    
    while q:
        time += 1
        suma -= q.popleft()
        if truck_weights:
            if suma + truck_weights[0] <= weight:
                suma += truck_weights[0]        # 개어이 없네 .... sum 개 오래걸림...
                q.append(truck_weights.pop(0))
            else:
                q.append(0)
    
    return time
~~~