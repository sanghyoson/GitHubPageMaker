---
layout: post
current: post
cover:  assets/built/images/programmers_logo.jpg
navigation: True
title: 프로그래머스 - 전력망 둘로 나누기(BFS, DFS)
date: 2022-01-02 12:40:00
tags: [programmers, dfs bfs]
class: post-template
subclass: 'post tag-python'
author: sanghyoson
---
<i class="fa fa-search">&nbsp;</i> 
<a href='https://programmers.co.kr/learn/courses/30/lessons/86971'> BFS, DFS - 전력망 둘로 나누기</a>
![프로그래머스 사진](../assets/built/images/programmers_logo.jpg){: width="100%" height="100%"}

<h2>문제 설명</h2>
<br/>
n개의 송전탑이 전선을 통해 하나의 트리 형태로 연결되어 있습니다. 당신은 이 전선들 중 하나를 끊어서 현재의 전력망 네트워크를 2개로 분할하려고 합니다. 이때, 두 전력망이 갖게 되는 송전탑의 개수를 최대한 비슷하게 맞추고자 합니다.

송전탑의 개수 n, 그리고 전선 정보 wires가 매개변수로 주어집니다. 전선들 중 하나를 끊어서 송전탑 개수가 가능한 비슷하도록 두 전력망으로 나누었을 때, 두 전력망이 가지고 있는 송전탑 개수의 차이(절대값)를 return 하도록 solution 함수를 완성해주세요.


<br/>

<h2>제한 사항</h2>
<ul class = 'data-contents'>
<br/>
<li>n은 2 이상 100 이하인 자연수입니다.</li>
<li>wires는 길이가 n-1인 정수형 2차원 배열입니다.</li>
<li>wires의 각 원소는 [v1, v2] 2개의 자연수로 이루어져 있으며, 이는 전력망의 v1번 송전탑과 v2번 송전탑이 전선으로 연결되어 있다는 것을 의미합니다.</li>
<li>1 ≤ v1 < v2 ≤ n 입니다.</li>
<li>전력망 네트워크가 하나의 트리 형태가 아닌 경우는 입력으로 주어지지 않습니다.</li>
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
이 역시 DFS, BFS 를 이용하면 풀수 있다. 아이디어는 쉽게 나오는데, 코드 자체가 익숙하지 않다. 특히 DFS, BFS 작성이 조금 어렵다. 이를 중점으로 공부해야할 듯.
그래프를 생성해서, DFS 혹은 BFS를 통해 이어져 있는 노드를 모두 탐색하고, 이 값과 다른 망의 크기가 어느정도 차이가나는지만 구하면 된다.
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
~~~javascript
function solution(n, wires) {
    function dfs(graph, visited, start){
        let stack = [start];
        let cnt = 0;
        while (stack.length){
            let node = stack.pop();
            if (visited[node] == false) {
                visited[node] = true;
                cnt += 1;
            }
            
            for (let i = 1; i <= n; i++){
                if (visited[i] == false && graph[node][i] == 1){
                    stack.push(i);
                }
            }
        }
        return cnt;
    }
    let tmp = [];
    wires.forEach(delWire => {
                let visited = Array(n+1).fill(false);
                let selected_wires = wires.filter( x => x !== delWire);
                let link = 0;
                let graph = Array.from(Array(n+1), ()=> Array(n+1).fill(0));
                selected_wires.forEach((v)=> {
                    graph[v[0]][v[1]] = 1;
                    graph[v[1]][v[0]] = 1;
                })
                for (let i = 1; i <= n; i++){
                    if (visited[i] == false){
                        link = dfs(graph, visited, i);
                    }
                }
                tmp.push(link);
    })
    tmp = tmp.map(v => Math.abs(n-v-v) );
    return Math.min(...tmp);
}
~~~
