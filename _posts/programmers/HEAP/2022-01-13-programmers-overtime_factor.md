---
layout: post
current: post
cover:  assets/built/images/programmers_logo.jpg
navigation: True
title: 프로그래머스 - 야근 지수(Heap)
date: 2022-01-13 12:40:00
tags: [programmers, heap]
class: post-template
subclass: 'post tag-python'
author: sanghyoson
---
<i class="fa fa-search">&nbsp;</i> 
<a href='https://programmers.co.kr/learn/courses/30/lessons/42628'> Heap - 야근 지수</a>
![프로그래머스 사진](../assets/built/images/programmers_logo.jpg){: width="100%" height="100%"}

<h2>문제 설명</h2>
<br/>
회사원 Demi는 가끔은 야근을 하는데요, 야근을 하면 야근 피로도가 쌓입니다. 야근 피로도는 야근을 시작한 시점에서 남은 일의 작업량을 제곱하여 더한 값입니다. Demi는 N시간 동안 야근 피로도를 최소화하도록 일할 겁니다.Demi가 1시간 동안 작업량 1만큼을 처리할 수 있다고 할 때, 퇴근까지 남은 N 시간과 각 일에 대한 작업량 works에 대해 야근 피로도를 최소화한 값을 리턴하는 함수 solution을 완성해주세요.

|works|n|result|
|---|---|---|
|[4,3,4]|4|12|
|[2,1,2]|1|6|
|[1,1]|3|0|

<br/>
<h2>제한 사항</h2>
<ul class = 'data-contents'>
<br/>
<li>works는 길이 1 이상, 20,000 이하인 배열입니다.</li>
<li>works의 원소는 50000 이하인 자연수입니다.</li>
<li>n은 1,000,000 이하인 자연수입니다.</li>
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
일단 n 100만, 배열 길이가 5만이기 때문에 완전 탐색과 같은 방법은 당연히 불가능하다. 빠르게 해결할 수 있는 방법은 야근 지수가 남은 작업량의 지수로 증가하는 것을 고려하여 최대값을 찾아 최대값을 줄여나가는 방향으로 진행하면 되겠다. 일단, 방법은 해당방법을 진행하였는데, 초기에 최대 인덱스를 찾는 max, index 등의 함수를 이용하여 해결하였으나, 시간초과. sort 함수를 이용해서 맨 끝 값을 감소시키는 방향도 역시 시간 초과였다. 조금 더 빠른 방법을 고려하여 최대값을 탐색하기 때문에, Heap 을 이용하는 방법을 이용하였다. 하지만 본인이 작성한 Heap 코드는 역시 효율성이 떨어지는 것 같다... 역시 시간 초과. 


다른 사람들의 풀이를 보니 heapq등의 빌트인 함수를 사용하면 되는것 같다.

<!-- <ol class = 'data-contents'>
    <li>1. 가장 큰 수를 제거</li>
    <li>2. 시간 포인트(시작, 종료시간)에서 오버랩되는 데이터의 수 카운트하기</li>
</ol>
<br/> -->

<!-- <h4>풀이과정 - 문자열로부터 시작, 종료 시간 파싱하기</h4>
<br/>
문자열로부터 원하는 숫자를 뽑아내는 파싱 과정 통해서 각 로그 데이터의 시작, 종료 시간을 구하는 것은 간단하다. 종료 시간에서 데이터 처리 시간을 빼면 시작 시간을 구할 수 있다. 다만, 해당 문제에서의 **핵심은 기본 환산단위를 ms로 변경**하는 과정인 것 같다.
문제 자체를 해결함에 있어서는 ms로의 환산이 크게 중요하지 않지만, 소수점으로 인해서 연산 중 오차가 발생하는 것을 확인하였다. (소수점 연산 속도 차이도 있을 것 같다.)  -->

<!-- <h4>풀이과정 2 - 시간 포인트(시작, 종료시간)에서 오버랩되는 데이터의 수 카운트하기</h4>
<br/>
초기 접근 방법은 1초간의 윈도우를 슬라이딩하며 각 윈도우에서 오버랩되는 데이터 수를 카운트하는 방법이었다. 해당 방법으로 원하는 결과를 얻을 수는 있지만, 효율성 측면에서 매우 떨어진다. 해당 **문제의 기본 시간 단위는 ms**이므로, 1초 동안 슬라이딩을 진행하여도 최소 1000번의 알고리즘이 진행되게 되고, 오버랩되는 카운터를 고려한다면 알고리즘 진행 시간은 더욱 늘어난다. 제안한 알고리즘의 **요청량이 변화하는 시점은 로그의 시작점, 종료점** 뿐이라는 점을 이용한다. 요청량이 변화는 전체 로그에서 시작, 종료점에서만 발생하므로, 해당 지점에서의 최대 요청량을 구하면, 전체 로그의 최대 요청량을 구할 수 있다. 따라서, 전체 시간을 슬라이딩 시키지 않고, 로그 시작, 종료점에서만 진행하여 구하였다.
<br/> -->


<h2>최종 코드</h2>
~~~python
def solution(n, works):
    
    for _ in range(n):
        m = max(works)
        if m > 0:
            works[works.index(max(works))] -= 1
    
    answer = [i**2 for i in works]
    return sum(answer)
}
~~~

<h2>힙을 이용한 코드</h2>
~~~python
def solution(n, works):

    h = MaxHeap()
    for i in works:
        h.insert(i)
        
    for _ in range(n):
        M = h.remove()
        if M > 0:
            h.insert(M-1)
    
    tmp = h.queue[1:]
    answer = [i**2 for i in tmp]
    return sum(answer)

class MaxHeap:
    def __init__(self):
        self.queue = [None]
    
    def swap(self, ai, bi):
        self.queue[ai], self.queue[bi] = self.queue[bi], self.queue[ai]
        
    def insert(self, data):
        self.queue.append(data)
        curInx = len(self.queue) - 1
        parInx = curInx // 2
        while curInx != 1:
            if self.queue[curInx] > self.queue[parInx]:
                self.swap(curInx, parInx)
                curInx = parInx
                parInx = curInx // 2
            else:
                break
        
    def remove(self):
        if len(self.queue) > 1:
            self.swap(1, -1)
            data = self.queue.pop()
            self.maxHeapify(1)
        else:
            data = None
        return data
    
    def maxHeapify(self, i):
        leftInx = 2*i
        rightInx = 2*i + 1
        biggest = i
        
        if leftInx < len(self.queue) and self.queue[leftInx] > self.queue[biggest]:
            biggest = leftInx
        if rightInx < len(self.queue) and self.queue[rightInx] > self.queue[biggest]:
            biggest = rightInx
        if biggest != i:
            self.swap(biggest, i)
            self.maxHeapify(biggest)
~~~