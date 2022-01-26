---
layout: post
current: post
cover:  assets/built/images/programmers_logo.jpg
navigation: True
title: 프로그래머스 - 이중우선순위큐(Heap)
date: 2021-12-15 12:40:00
tags: [programmers, heap]
class: post-template
subclass: 'post tag-python'
author: sanghyoson
---
<i class="fa fa-search">&nbsp;</i> 
<a href='https://programmers.co.kr/learn/courses/30/lessons/42628'> Heap - 이중우선순위큐</a>
![프로그래머스 사진](../assets/built/images/programmers_logo.jpg){: width="100%" height="100%"}

<h2>문제 설명</h2>
<br/>
이중 우선순위 큐는 다음 연산을 할 수 있는 자료구조를 말합니다.

|명령어|수신|탑(높이)|
|---|---|---|
|I |숫자|	큐에 주어진 숫자를 삽입합니다.|
|D |1	|큐에서 최댓값을 삭제합니다.|
|D |-1|	큐에서 최솟값을 삭제합니다.|

이중 우선순위 큐가 할 연산 operations가 매개변수로 주어질 때, 모든 연산을 처리한 후 큐가 비어있으면 [0,0] 비어있지 않으면 [최댓값, 최솟값]을 return 하도록 solution 함수를 구현해주세요.
<br/>

<h2>제한 사항</h2>
<ul class = 'data-contents'>
<br/>
<li>operations는 길이가 1 이상 1,000,000 이하인 문자열 배열입니다.</li>
<li>operations의 원소는 큐가 수행할 연산을 나타냅니다.</li>
<li>원소는 “명령어 데이터” 형식으로 주어집니다.- 최댓값/최솟값을 삭제하는 연산에서 최댓값/최솟값이 둘 이상인 경우, 하나만 삭제합니다.</li>
<li>빈 큐에 데이터를 삭제하라는 연산이 주어질 경우, 해당 연산은 무시합니다.</li>
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
큐를 이용하되, 큐를 크기 순으로 정렬해 놓으면, 최대 최소를 처리하기 간편하다. 그게 전부?
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
~~~javascript
function solution(operations) {
    let q = [];
    
    for (const op of operations) {
        let opl = op.split(' ');
        
        if (opl[0] == 'I'){
            q.push(Number(opl[1]))
            q.sort((a,b)=> b-a);
        } else {
            if (opl[1] == 1) {
                q.shift();
            } else {
                q.pop();
            }
        }
    }
    
    return q.length == 0 ? [0,0] : [q[0], q[q.length - 1]];
}
~~~

