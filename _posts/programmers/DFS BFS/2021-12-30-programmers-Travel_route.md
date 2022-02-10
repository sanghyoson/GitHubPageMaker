---
layout: post
current: post
cover:  assets/built/images/programmers_logo.jpg
navigation: True
title: 프로그래머스 - 여행 경로(BFS, DFS)
date: 2021-12-30 12:40:00
tags: [programmers, dfs bfs]
class: post-template
subclass: 'post tag-python'
author: sanghyoson
---
<i class="fa fa-search">&nbsp;</i> 
<a href='https://programmers.co.kr/learn/courses/30/lessons/43164'> BFS, DFS - 여행 경로</a>
![프로그래머스 사진](../assets/built/images/programmers_logo.jpg){: width="100%" height="100%"}

<h2>문제 설명</h2>
<br/>
주어진 항공권을 모두 이용하여 여행경로를 짜려고 합니다. 항상 "ICN" 공항에서 출발합니다.

항공권 정보가 담긴 2차원 배열 tickets가 매개변수로 주어질 때, 방문하는 공항 경로를 배열에 담아 return 하도록 solution 함수를 작성해주세요.
<br/>

<h2>제한 사항</h2>
<ul class = 'data-contents'>
<br/>
<li>모든 공항은 알파벳 대문자 3글자로 이루어집니다.</li>
<li>주어진 공항 수는 3개 이상 10,000개 이하입니다.</li>
<li>tickets의 각 행 [a, b]는 a 공항에서 b 공항으로 가는 항공권이 있다는 의미입니다.</li>
<li>주어진 항공권은 모두 사용해야 합니다.</li>
<li>만일 가능한 경로가 2개 이상일 경우 알파벳 순서가 앞서는 경로를 return 합니다.</li>
<li>모든 도시를 방문할 수 없는 경우는 주어지지 않습니다.</li>
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
DFS, BFS 를 이용하여 풀어야한다는 것은 이해... 하지만, 코드를 능숙하게 짜는 법을 모르곘다... 타인의 코드를 보면 별 어려움없이 해석은 가능 ...
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
function solution(tickets){
       let routes = [];  
                       
       function dfs (extraTickets, currentLocation,route ) {
            if(extraTickets.length===0){
           		routes.push(route);
            }
            else{
                extraTickets.forEach(([departure, destination], index) => {
                   if( currentLocation === departure){
                        const newTickets = extraTickets.filter((v,i)=> i !== index);
                        dfs(newTickets, destination, [...route, destination])
                    }
                });
            }
        }
        dfs(tickets , "ICN" , ["ICN"])
        return  routes.sort()[0];
    }
~~~
<br/>


<h2>최종 코드2 -- 중복되는 티켓이 있을 경우 통과 안돼 ... </h2>
~~~python
def solution(tickets):
    paths = []
    def dfs(tickets, visited, cur, path):      # 리스트는 콜 바이 레프 인데... 다 찾아낼까 ..?
        if len(path) == len(tickets) + 1:
            if path not in paths:
                paths.append(path)
            return

        for ticket in tickets:
            if ticket not in visited:
                depature, arrival = ticket
                if depature == cur:
                    newVisted = visited[:]
                    newVisted.append(ticket)
                    newPath = path[:]
                    newPath.append(arrival)
                    dfs(tickets, newVisted, arrival, newPath)
    
    dfs(tickets, [], 'ICN', ['ICN'])
    paths.sort()
    return paths[0]
~~~
