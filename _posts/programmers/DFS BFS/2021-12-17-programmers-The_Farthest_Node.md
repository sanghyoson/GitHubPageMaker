---
layout: post
current: post
cover:  assets/built/images/programmers_logo.jpg
navigation: True
title: 프로그래머스 - 가장 먼 노드(BFS, DFS)
date: 2021-12-17 12:40:00
tags: [programmers, binary search]
class: post-template
subclass: 'post tag-python'
author: sanghyoson
---
<i class="fa fa-search">&nbsp;</i> 
<a href='https://programmers.co.kr/learn/courses/30/lessons/49189'> BFS, DFS - 가장 먼 노드</a>
![프로그래머스 사진](../assets/built/images/programmers_logo.jpg){: width="100%" height="100%"}

<h2>문제 설명</h2>
<br/>
n개의 노드가 있는 그래프가 있습니다. 각 노드는 1부터 n까지 번호가 적혀있습니다. 1번 노드에서 가장 멀리 떨어진 노드의 갯수를 구하려고 합니다. 가장 멀리 떨어진 노드란 최단경로로 이동했을 때 간선의 개수가 가장 많은 노드들을 의미합니다.

노드의 개수 n, 간선에 대한 정보가 담긴 2차원 배열 vertex가 매개변수로 주어질 때, 1번 노드로부터 가장 멀리 떨어진 노드가 몇 개인지를 return 하도록 solution 함수를 작성해주세요.

<br/>

<h2>입력 형식</h2>
<ul class = 'data-contents'>
<br/>
<li>노드의 개수 n은 2 이상 20,000 이하입니다.</li>
<li>간선은 양방향이며 총 1개 이상 50,000개 이하의 간선이 있습니다.</li>
<li>vertex 배열 각 행 [a, b]는 a번 노드와 b번 노드 사이에 간선이 있다는 의미입니다.</li>
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
처음 시작하는 노드인 '1'에서부터 시작하여, 모든 노드를 탐색하여, 각 노드까지의 거리를 결정하여야 한다. 따라서 모든 탐색을 위한 BFS나 DFS가 필요하다고 판단했다. 다만, 가장 깊은 노드들의 집합을 알아 내는 것이 목표이므로 같은 깊이를 탐색하는 BFS가 DFS보다는 적합하다. 

<ol class = 'data-contents'>
    <li>1. 배열로 주어진 데이터를 이용하여 그래프로 표현한다.</li>
    <li>2. BFS를 이용하여 탐색을 시작하고, 탐색을 통해 거쳐가는 노드들의 깊이를 담은 배열을 구한다.</li>
    <li>3. 탐색이 종료되면, 가장 거리가 먼 노드의 개수를 구한다.</li>
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
function solution(n, edge) {
    const graph = Array.from(
        Array(n+1),
        () => []
    );
    
    for (const [st, en] of edge){
        graph[st].push(en);
        graph[en].push(st);
    }           
    
    
    const distance = Array(n+1).fill(0);
    distance[1] = 1;
    
    const q = [1];
    while (q.length > 0){
        const st = q.shift();
        for (const en of graph[st]){
            if (distance[en] === 0){
                q.push(en);
                distance[en] = distance[st] + 1;
            }
        }
    }
    const max = Math.max(...distance);
    return distance.filter(x => x === max).length;
}
~~~
