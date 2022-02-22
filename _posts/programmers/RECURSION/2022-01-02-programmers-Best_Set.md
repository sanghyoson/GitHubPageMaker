---
layout: post
current: post
cover:  assets/built/images/programmers_logo.jpg
navigation: True
title: 프로그래머스 - 최고의 집합 (Recursion)
date: 2021-12-23 12:40:00
tags: [programmers, recursion]
class: post-template
subclass: 'post tag-python'
author: sanghyoson
---
<i class="fa fa-search">&nbsp;</i> 
<a href='https://programmers.co.kr/learn/courses/30/lessons/42839?language=javascript'> Recursion - 최고의 집합</a>
![프로그래머스 사진](../assets/built/images/programmers_logo.jpg){: width="100%" height="100%"}

<h2>문제 설명</h2>
<br/>
자연수 n 개로 이루어진 중복 집합(multi set, 편의상 이후에는 "집합"으로 통칭) 중에 다음 두 조건을 만족하는 집합을 최고의 집합이라고 합니다.

각 원소의 합이 S가 되는 수의 집합
위 조건을 만족하면서 각 원소의 곱 이 최대가 되는 집합
예를 들어서 자연수 2개로 이루어진 집합 중 합이 9가 되는 집합은 다음과 같이 4개가 있습니다.
{ 1, 8 }, { 2, 7 }, { 3, 6 }, { 4, 5 }
그중 각 원소의 곱이 최대인 { 4, 5 }가 최고의 집합입니다.

집합의 원소의 개수 n과 모든 원소들의 합 s가 매개변수로 주어질 때, 최고의 집합을 return 하는 solution 함수를 완성해주세요.
<br/>

<h2>제한 사항</h2>
<ul class = 'data-contents'>
<br/>
<li>최고의 집합은 오름차순으로 정렬된 1차원 배열(list, vector) 로 return 해주세요.</li>
<li>만약 최고의 집합이 존재하지 않는 경우에 크기가 1인 1차원 배열(list, vector) 에 -1 을 채워서 return 해주세요.</li>
<li>자연수의 개수 n은 1 이상 10,000 이하의 자연수입니다.</li>
<li>모든 원소들의 합 s는 1 이상, 100,000,000 이하의 자연수입니다.</li>
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
s가 최대 1억, n 도 1만개의 개수를 갖기 때문에, 완전탐색으로는 어려움이 있다. 다만, 초기 접근은 완전 탐색을 통해서 전체 집합을 구해보는 것이 목적이었기 때문에 재귀를 이용하여 완전 탐색을 하였다. 결과적으로는 제대로 된 집합을 구할 수 있으나, n이 7개만 넘어가도 탐색시 10초 이상을 소요한다. 실제 통과를 위한 접근 방법은 집합들의 합이 같을 때, 각 값들의 차가 적을 때에 곱이 가장 큼을 이용했다.
<!-- <ol class = 'data-contents'>
    <li>1. number의 맨 앞의 자리의 수를 임시로 데이터를 저장하는 stack에 저장한다.</li>
    <li>2. stack 데이터와 number의 다음 자리수를 비교하는데, stack 내의 데이터가 작으면 이를 제거하고 카운트를 증가시키고 그렇지 않으면 stack에 그 number의 그 다음자리를 저장한다.</li>
    <li>3. 위를 반복하여, 카운터가 k와 같으면 알고리즘을 종료하고 stack과 남은 number를 이어붙여 return한다.</li>
</ol>
<br/>
    JS에서는 제공하지 않는 큐를 사용하였는데, deque를 사용하는 것이 번거로워 reverse()한 후, pop()을 사용하였다. -->

<!-- <h4>풀이과정 - 문자열로부터 시작, 종료 시간 파싱하기</h4>
<br/>
문자열로부터 원하는 숫자를 뽑아내는 파싱 과정 통해서 각 로그 데이터의 시작, 종료 시간을 구하는 것은 간단하다. 종료 시간에서 데이터 처리 시간을 빼면 시작 시간을 구할 수 있다. 다만, 해당 문제에서의 **핵심은 기본 환산단위를 ms로 변경**하는 과정인 것 같다.
문제 자체를 해결함에 있어서는 ms로의 환산이 크게 중요하지 않지만, 소수점으로 인해서 연산 중 오차가 발생하는 것을 확인하였다. (소수점 연산 속도 차이도 있을 것 같다.)  -->

<!-- <h4>풀이과정 2 - 시간 포인트(시작, 종료시간)에서 오버랩되는 데이터의 수 카운트하기</h4>
<br/>
초기 접근 방법은 1초간의 윈도우를 슬라이딩하며 각 윈도우에서 오버랩되는 데이터 수를 카운트하는 방법이었다. 해당 방법으로 원하는 결과를 얻을 수는 있지만, 효율성 측면에서 매우 떨어진다. 해당 **문제의 기본 시간 단위는 ms**이므로, 1초 동안 슬라이딩을 진행하여도 최소 1000번의 알고리즘이 진행되게 되고, 오버랩되는 카운터를 고려한다면 알고리즘 진행 시간은 더욱 늘어난다. 제안한 알고리즘의 **요청량이 변화하는 시점은 로그의 시작점, 종료점** 뿐이라는 점을 이용한다. 요청량이 변화는 전체 로그에서 시작, 종료점에서만 발생하므로, 해당 지점에서의 최대 요청량을 구하면, 전체 로그의 최대 요청량을 구할 수 있다. 따라서, 전체 시간을 슬라이딩 시키지 않고, 로그 시작, 종료점에서만 진행하여 구하였다.
<br/> -->
<br/>


<h2>완전 탐색 코드</h2>
~~~python
def multifly(data):
    answer = 1
    for i in data:
        answer *= i
    return answer

def solution(n, s):
    tmp = []
    
    def makeSet(dataSet = []):
        if len(dataSet) == n:
            if sum(dataSet) == s:
                sortedDataSet = dataSet[:]
                sortedDataSet.sort()
                if sortedDataSet not in tmp:
                    tmp.append(sortedDataSet)
        else:
            for i in range(1, s+1):
                newDataSet = dataSet[:]
                newDataSet.append(i)
                makeSet(newDataSet)
    
    makeSet()
    
    if len(tmp) == 0:
        return [-1]
    else:
        mSet = []
        for data in tmp:
            mSet.append(multifly(data))
        return tmp[mSet.index(max(mSet))]
~~~

<br/>
<h2>통과 코드</h2>
~~~python
def solution(n, s):
    if n > s:
        return [-1]
    [portion, remain] = divmod(s, n)
    answer = [portion] * n
    for i in range(remain):
        answer[i] += 1
    return sorted(answer)
~~~
<br/>