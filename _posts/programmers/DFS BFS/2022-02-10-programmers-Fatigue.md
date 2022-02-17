---
layout: post
current: post
cover:  assets/built/images/programmers_logo.jpg
navigation: True
title: 프로그래머스 - 피로도(BFS, DFS)
date: 2022-02-10 12:40:00
tags: [programmers, dfs bfs]
class: post-template
subclass: 'post tag-python'
author: sanghyoson
---
<i class="fa fa-search">&nbsp;</i> 
<a href='https://programmers.co.kr/learn/courses/30/lessons/87946'> BFS, DFS - 피로도</a>
![프로그래머스 사진](../assets/built/images/programmers_logo.jpg){: width="100%" height="100%"}

<h2>문제 설명</h2>
<br/>
XX게임에는 피로도 시스템(0 이상의 정수로 표현합니다)이 있으며, 일정 피로도를 사용해서 던전을 탐험할 수 있습니다. 이때, 각 던전마다 탐험을 시작하기 위해 필요한 "최소 필요 피로도"와 던전 탐험을 마쳤을 때 소모되는 "소모 피로도"가 있습니다. "최소 필요 피로도"는 해당 던전을 탐험하기 위해 가지고 있어야 하는 최소한의 피로도를 나타내며, "소모 피로도"는 던전을 탐험한 후 소모되는 피로도를 나타냅니다. 예를 들어 "최소 필요 피로도"가 80, "소모 피로도"가 20인 던전을 탐험하기 위해서는 유저의 현재 남은 피로도는 80 이상 이어야 하며, 던전을 탐험한 후에는 피로도 20이 소모됩니다.

이 게임에는 하루에 한 번씩 탐험할 수 있는 던전이 여러개 있는데, 한 유저가 오늘 이 던전들을 최대한 많이 탐험하려 합니다. 유저의 현재 피로도 k와 각 던전별 "최소 필요 피로도", "소모 피로도"가 담긴 2차원 배열 dungeons 가 매개변수로 주어질 때, 유저가 탐험할수 있는 최대 던전 수를 return 하도록 solution 함수를 완성해주세요.

<br/>

<h2>제한 사항</h2>
<ul class = 'data-contents'>
<br/>
<li>k는 1 이상 5,000 이하인 자연수입니다.</li>
<li>dungeons의 세로(행) 길이(즉, 던전의 개수)는 1 이상 8 이하입니다.</li>
<li>dungeons의 가로(열) 길이는 2 입니다.</li>
<li>dungeons의 각 행은 각 던전의 ["최소 필요 피로도", "소모 피로도"] 입니다.</li>
<li>"최소 필요 피로도"는 항상 "소모 피로도"보다 크거나 같습니다.</li>
<li>"최소 필요 피로도"와 "소모 피로도"는 1 이상 1,000 이하인 자연수입니다.</li>
<li>서로 다른 던전의 ["최소 필요 피로도", "소모 피로도"]가 서로 같을 수 있습니다.</li>
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
DFS 접근 방법, 결과, visited 등을 이용하면 접근할 수 있다. 다만, 파이썬에서는 list의 경우 Call by Ref로서 접근한다. 때문에, DFS 순환시 이를 고려하지 않으면 모든 경로를 탐색할 수 없다. Call by Ref를 회피할 수 있는 방안을 생각하자.
<!-- <oㅇㄹl class = 'data-contents'>
    <li>1. 시작노드에서 다음노드를 탐색하고 방문 처리한다.</li>
    <li>2. 그 위치에서 또 다시 방문하지 않은 노드를 탐색하고 방문 처리힌디.</li>
    <li>3. 더이상 해당 그룹에서 방문할 수 없을 경우 새로운 노드로부터 1~3을 반복한다.</li>
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
<br/>


<h2>최종 코드</h2>
~~~python
def solution(k, dungeons):
    answer = 0
    N = len(dungeons)
    visited = [0 for _ in range(N)]
    
    def dfs(k, cnt, visited):
        nonlocal answer
        if cnt > answer:
            answer = cnt

        for j in range(N):
            if k >= dungeons[j][0] and not visited[j]:
                newVisited = visited[:]
                newVisited[j] = 1
                dfs(k - dungeons[j][1], cnt + 1, newVisited)
                
    dfs(k, 0, visited)
    return answer
~~~
