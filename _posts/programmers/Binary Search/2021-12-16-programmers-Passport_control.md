---
layout: post
current: post
cover:  assets/built/images/programmers_logo.jpg
navigation: True
title: 프로그래머스 - 입국 심사(Binary Search)
date: 2021-12-16 12:40:00
tags: [programmers, binary search]
class: post-template
subclass: 'post tag-python'
author: sanghyoson
---
<i class="fa fa-search">&nbsp;</i> 
<a href='https://programmers.co.kr/learn/courses/30/lessons/43238?language=javascript'> Binary Search - 입국심사</a>
![프로그래머스 사진](../assets/built/images/programmers_logo.jpg){: width="100%" height="100%"}

<h2>문제 설명</h2>
<br/>
n명이 입국심사를 위해 줄을 서서 기다리고 있습니다. 각 입국심사대에 있는 심사관마다 심사하는데 걸리는 시간은 다릅니다.

처음에 모든 심사대는 비어있습니다. 한 심사대에서는 동시에 한 명만 심사를 할 수 있습니다. 가장 앞에 서 있는 사람은 비어 있는 심사대로 가서 심사를 받을 수 있습니다. 하지만 더 빨리 끝나는 심사대가 있으면 기다렸다가 그곳으로 가서 심사를 받을 수도 있습니다.

모든 사람이 심사를 받는데 걸리는 시간을 최소로 하고 싶습니다.

입국심사를 기다리는 사람 수 n, 각 심사관이 한 명을 심사하는데 걸리는 시간이 담긴 배열 times가 매개변수로 주어질 때, 모든 사람이 심사를 받는데 걸리는 시간의 최솟값을 return 하도록 solution 함수를 작성해주세요.

<br/>

<h2>입력 형식</h2>
<ul class = 'data-contents'>
<br/>
<li>입국심사를 기다리는 사람은 1명 이상 1,000,000,000명 이하입니다.</li>
<li>각 심사관이 한 명을 심사하는데 걸리는 시간은 1분 이상 1,000,000,000분 이하입니다.</li>
<li>심사관은 1명 이상 100,000명 이하입니다.</li>
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
최종적으로 소요되는 시간을 도출 해야한다. 다만, 제한사항에서 입국 심사를 받는 사람의 수(n)와 심사시간의 크기가 크기 때문에, 효율적으로 탐색해야 한다. 여기서는 이분 탐색으로 접근하였다. 해당 문제를 해결하기 위한 알고리즘 순서는 다음과 같다.

<ol class = 'data-contents'>
    <li>1. 이분 탐색을 위해서 (시간)데이터를 정렬한다.</li>
    <li>2. left를 최소 시간인 1분, right를 최대 시간(최대 시간이란, 입국하는 모든 사람이 심사시간이 가장 긴 심사관에게 심사를 받는 경우)으로 결정한다.</li>
    <li>3. 중간 시간일 떄, 심사받을 수 있는 사람이 n보다 큰지, 혹은 작은지를 판단하여 left(or right)를 변경한다.</li>
</ol>
<br/>

<!-- <h4>풀이과정 - 문자열로부터 시작, 종료 시간 파싱하기</h4>
<br/>
문자열로부터 원하는 숫자를 뽑아내는 파싱 과정 통해서 각 로그 데이터의 시작, 종료 시간을 구하는 것은 간단하다. 종료 시간에서 데이터 처리 시간을 빼면 시작 시간을 구할 수 있다. 다만, 해당 문제에서의 **핵심은 기본 환산단위를 ms로 변경**하는 과정인 것 같다.
문제 자체를 해결함에 있어서는 ms로의 환산이 크게 중요하지 않지만, 소수점으로 인해서 연산 중 오차가 발생하는 것을 확인하였다. (소수점 연산 속도 차이도 있을 것 같다.)  -->

<!-- <h4>풀이과정 2 - 시간 포인트(시작, 종료시간)에서 오버랩되는 데이터의 수 카운트하기</h4>
<br/>
초기 접근 방법은 1초간의 윈도우를 슬라이딩하며 각 윈도우에서 오버랩되는 데이터 수를 카운트하는 방법이었다. 해당 방법으로 원하는 결과를 얻을 수는 있지만, 효율성 측면에서 매우 떨어진다. 해당 **문제의 기본 시간 단위는 ms**이므로, 1초 동안 슬라이딩을 진행하여도 최소 1000번의 알고리즘이 진행되게 되고, 오버랩되는 카운터를 고려한다면 알고리즘 진행 시간은 더욱 늘어난다. 제안한 알고리즘의 **요청량이 변화하는 시점은 로그의 시작점, 종료점** 뿐이라는 점을 이용한다. 요청량이 변화는 전체 로그에서 시작, 종료점에서만 발생하므로, 해당 지점에서의 최대 요청량을 구하면, 전체 로그의 최대 요청량을 구할 수 있다. 따라서, 전체 시간을 슬라이딩 시키지 않고, 로그 시작, 종료점에서만 진행하여 구하였다.
<br/> -->
<br/>


<h2>최종 코드</h2>
~~~javascript
function solution(n, times) {
    const sortedTimes = times.sort((a,b) => a - b);
    let left = 1;
    let right = sortedTimes[sortedTimes.length - 1] * n;
    
    while (left <= right){
        const mid = Math.floor((left+right)/2);
        const sum = times.reduce((acc, time) => acc + Math.floor(mid / time),0);
        
        if (sum < n){
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    
    return left;
}
~~~
<br/>

~~~python
def solution(n, times):
    answer = 0
    left = 1
    right = max(times) * n
    
    while left <= right:
        mid = (left + right) // 2
        person_cnt = 0
        
        for time in times:
            person_cnt += mid // time
            if person_cnt >= n:
                break
        
        if person_cnt >= n:
            right = mid - 1
            answer = mid
        else:
            left = mid + 1
    
    return answer
~~~

