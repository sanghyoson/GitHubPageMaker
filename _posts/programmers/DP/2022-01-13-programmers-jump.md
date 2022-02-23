---
layout: post
current: post
cover:  assets/built/images/programmers_logo.jpg
navigation: True
title: 프로그래머스 - 멀리 뛰기 (dp)
date: 2022-01-13 12:40:00
tags: [programmers, dp]
class: post-template
subclass: 'post tag-python'
author: sanghyoson
---
<i class="fa fa-search">&nbsp;</i> 
<a href='https://programmers.co.kr/learn/courses/30/lessons/12914'> DP - 멀리 뛰기</a>
![프로그래머스 사진](../assets/built/images/programmers_logo.jpg){: width="100%" height="100%"}

<h2>문제 설명</h2>
<br/>
단효진이는 멀리 뛰기를 연습하고 있습니다. 효진이는 한번에 1칸, 또는 2칸을 뛸 수 있습니다. 칸이 총 4개 있을 때, 효진이는
(1칸, 1칸, 1칸, 1칸)
(1칸, 2칸, 1칸)
(1칸, 1칸, 2칸)
(2칸, 1칸, 1칸)
(2칸, 2칸)
의 5가지 방법으로 맨 끝 칸에 도달할 수 있습니다. 멀리뛰기에 사용될 칸의 수 n이 주어질 때, 효진이가 끝에 도달하는 방법이 몇 가지인지 알아내, 여기에 1234567를 나눈 나머지를 리턴하는 함수, solution을 완성하세요. 예를 들어 4가 입력된다면, 5를 return하면 됩니다.
<br/>

<h2>제한 사항</h2>
<ul class = 'data-contents'>
<br/>
<li>n은 1 이상, 2000 이하인 정수입니다.</li>
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
초기 아이디어는 dfs를 이용하여, 모든 경우의 수를 탐색하는 방법이었다. 하지만 해당 방법은 시간 초과. 따라서 DP를 통합 문제 접근. 해당 규칙성을 확인해보면 피보나치 수열과 동일하다. 
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

<h2>DFS 풀이 코드</h2>
~~~python
def solution(n):
    answer = 0
    def dfs(result):
        if result == n:
            nonlocal answer
            answer += 1
        elif result < n:
            dfs(result + 1)
            dfs(result + 2)
    dfs(0)
    return answer%1234567
~~~
<br/>

<h2>참조 코드</h2>
~~~python
def solution(n):
    dp = [0, 1, 2]              // 순서 계산 귀찮아서, 0부터 시작
    if n < 3:
        return dp[n]
    else:
        for i in range(3,n+1):
            dp.append(dp[i-1] + dp[i-2])
            
    return dp[n]%1234567
~~~