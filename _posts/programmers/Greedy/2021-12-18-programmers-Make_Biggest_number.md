---
layout: post
current: post
cover:  assets/built/images/programmers_logo.jpg
navigation: True
title: 프로그래머스 - 큰 수 만들기(Greedy)
date: 2021-12-18 12:40:00
tags: [programmers, greedy]
class: post-template
subclass: 'post tag-python'
author: sanghyoson
---
<i class="fa fa-search">&nbsp;</i> 
<a href='https://programmers.co.kr/learn/courses/30/lessons/42883?language=javascript'> Greedy - 큰 수 만들기</a>
![프로그래머스 사진](../assets/built/images/programmers_logo.jpg){: width="100%" height="100%"}

<h2>문제 설명</h2>
<br/>
어떤 숫자에서 k개의 수를 제거했을 때 얻을 수 있는 가장 큰 숫자를 구하려 합니다.

예를 들어, 숫자 1924에서 수 두 개를 제거하면 [19, 12, 14, 92, 94, 24] 를 만들 수 있습니다. 이 중 가장 큰 숫자는 94 입니다.

문자열 형식으로 숫자 number와 제거할 수의 개수 k가 solution 함수의 매개변수로 주어집니다. number에서 k 개의 수를 제거했을 때 만들 수 있는 수 중 가장 큰 숫자를 문자열 형태로 return 하도록 solution 함수를 완성하세요.
<br/>

<h2>입력 형식</h2>
<ul class = 'data-contents'>
<br/>
<li>number는 1자리 이상, 1,000,000자리 이하인 숫자입니다.</li>
<li>k는 1 이상 number의 자릿수 미만인 자연수입니다.</li>
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
문제에서 주어진 k개를 삭제하여, 큰 수를 만드는 문제이다. 탐욕법(Greedy)을 이용하여 접근하면 쉽게 접근이 가능하다. 핵심은, 수의 맨 앞에서부터 작은 수를 차례로 제거하면 된다.  

<ol class = 'data-contents'>
    <li>1. number의 맨 앞의 자리의 수를 임시로 데이터를 저장하는 stack에 저장한다.</li>
    <li>2. stack 데이터와 number의 다음 자리수를 비교하는데, stack 내의 데이터가 작으면 이를 제거하고 카운트를 증가시키고 그렇지 않으면 stack에 그 number의 그 다음자리를 저장한다.</li>
    <li>3. 위를 반복하여, 카운터가 k와 같으면 알고리즘을 종료하고 stack과 남은 number를 이어붙여 return한다.</li>
</ol>
<br/>
    JS에서는 제공하지 않는 큐를 사용하였는데, deque를 사용하는 것이 번거로워 reverse()한 후, pop()을 사용하였다.

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
function solution(number, k) {
    let cnt = 0;
    let arr = number.split('');
    arr.reverse();
    let stack = [];
    while (cnt < k){
        if (stack.length == 0){
            stack.push(arr.pop());
        }
        
        if (arr.length == 0){
            stack.pop();
            cnt += 1;
        }

        if (stack[stack.length-1] < arr[arr.length-1]){
            stack.pop();
            cnt += 1;
        } else {
            stack.push(arr.pop());
        }
    }
    
    arr.reverse();
    return [...stack, ...arr].join('');
}
~~~


<br/>


<h2>다른 코드</h2>
~~~javascript
function solution(number, k) {
    const stack = [];
    let cnt = 0;
    
    for (const item of number){
        while (cnt < k && stack[stack.length-1] < item){
            stack.pop();
            cnt += 1;
        }
        stack.push(item);
    }
    
    // cnt가 쌓이지 않는 경우를 대비
    while (cnt < k){
        stack.pop();
        cnt += 1;
    }
    
    return stack.join('');
}
~~~
