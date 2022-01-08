---
layout: post
current: post
cover:  assets/built/images/programmers_logo.jpg
navigation: True
title: 프로그래머스 - 배달 (Dijkstra)
date: 2021-12-18 12:40:00
tags: [programmers, dijkstra]
class: post-template
subclass: 'post tag-python'
author: sanghyoson
---
<i class="fa fa-search">&nbsp;</i> 
<a href='https://programmers.co.kr/learn/courses/13213/lessons/91411'> Dijkstra - 배달</a>
![프로그래머스 사진](../assets/built/images/programmers_logo.jpg){: width="100%" height="100%"}

<h2>문제 설명</h2>
<br/>
N개의 마을로 이루어진 나라가 있습니다. 이 나라의 각 마을에는 1부터 N까지의 번호가 각각 하나씩 부여되어 있습니다. 각 마을은 양방향으로 통행할 수 있는 도로로 연결되어 있는데, 서로 다른 마을 간에 이동할 때는 이 도로를 지나야 합니다. 도로를 지날 때 걸리는 시간은 도로별로 다릅니다. 현재 1번 마을에 있는 음식점에서 각 마을로 음식 배달을 하려고 합니다. 각 마을로부터 음식 주문을 받으려고 하는데, N개의 마을 중에서 K 시간 이하로 배달이 가능한 마을에서만 주문을 받으려고 합니다. 다음은 N = 5, K = 3인 경우의 예시입니다.
1번 마을에 있는 음식점은 [1, 2, 4, 5] 번 마을까지는 3 이하의 시간에 배달할 수 있습니다. 그러나 3번 마을까지는 3시간 이내로 배달할 수 있는 경로가 없으므로 3번 마을에서는 주문을 받지 않습니다. 따라서 1번 마을에 있는 음식점이 배달 주문을 받을 수 있는 마을은 4개가 됩니다.
마을의 개수 N, 각 마을을 연결하는 도로의 정보 road, 음식 배달이 가능한 시간 K가 매개변수로 주어질 때, 음식 주문을 받을 수 있는 마을의 개수를 return 하도록 solution 함수를 완성해주세요.
<br/>

<h2>입력 형식</h2>
<ul class = 'data-contents'>
<br/>
<li>마을의 개수 N은 1 이상 50 이하의 자연수입니다.</li>
<li>road의 길이(도로 정보의 개수)는 1 이상 2,000 이하입니다.</li>
<li>road의 각 원소는 마을을 연결하고 있는 각 도로의 정보를 나타냅니다.</li>
<li>road는 길이가 3인 배열이며, 순서대로 (a, b, c)를 나타냅니다.</li>
<li>a, b(1 ≤ a, b ≤ N, a != b)는 도로가 연결하는 두 마을의 번호이며, c(1 ≤ c ≤ 10,000, c는 자연수)는 도로를 지나는데 걸리는 시간입니다.</li>
<li>두 마을 a, b를 연결하는 도로는 여러 개가 있을 수 있습니다.</li>
<li>한 도로의 정보가 여러 번 중복해서 주어지지 않습니다.</li>
<li>K는 음식 배달이 가능한 시간을 나타내며, 1 이상 500,000 이하입니다.</li>
<li>임의의 두 마을간에 항상 이동 가능한 경로가 존재합니다.</li>
<li>1번 마을에 있는 음식점이 K 이하의 시간에 배달이 가능한 마을의 개수를 return 하면 됩니다.</li>
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
열과 조합을 구할 때, 가장 간단한 방법은 반복되는 수만큼 반복문을 진행하는 것인데, 해당 방법은 순열, 조합에서의 k개의 반복문을 구해줘야 하기 때문에 매우 번거롭다. 따라서 순열과 조합의 경우 재귀문을 이용하면 쉽게 구할 수 있다고 한다.
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


<h2>최종 코드</h2>
~~~javascript
class MinHeap {
    constructor() {
        this.heap = [null];
    }

    push(value) {
        this.heap.push(value);
        let currentIndex = this.heap.length - 1;
        let parentIndex = Math.floor(currentIndex / 2);

        while (parentIndex !== 0 && this.heap[parentIndex].cost > value.cost) {
            const temp = this.heap[parentIndex];
            this.heap[parentIndex] = value;
            this.heap[currentIndex] = temp;

            currentIndex = parentIndex;
            parentIndex = Math.floor(currentIndex / 2);
        }
    }

    pop() {
        if (this.isEmpty()) return;
        if (this.heap.length === 2) return this.heap.pop();

        const returnValue = this.heap[1];
        this.heap[1] = this.heap.pop();

        let currentIndex  = 1;
        let leftIndex = 2;
        let rightIndex = 3;
        while ((this.heap[leftIndex] && this.heap[currentIndex].cost > this.heap[leftIndex].cost) || 
               (this.heap[rightIndex] && this.heap[currentIndex].cost > this.heap[rightIndex].cost)) {
            if (this.heap[leftIndex].cost > this.heap[rightIndex].cost) {
                const temp = this.heap[currentIndex];
                this.heap[currentIndex] = value;
                this.heap[rightIndex] = temp;
                currentIndex = rightIndex;
            } else {
                const temp = this.heap[currentIndex];
                this.heap[currentIndex] = value;
                this.heap[leftIndex] = temp;
                currentIndex = leftIndex;
            }
            leftIndex = currentIndex * 2;
            rightIndex = currentIndex * 2 + 1;
        }

        return returnValue;
    }

    isEmpty() {
        return this.heap.length === 1;
    }
}

function dijkstra(road, N) {
    const heap = new MinHeap(); // 우선순위 큐(힙)
    heap.push({ node: 1, cost: 0 }) // 1번 마을부터 시작

    const dist = [...Array(N + 1)].map(() => Infinity); // 계산하기 편하도록 N+1 길이만큼 리스트 생성
    dist[1] = 0; // 1번 마을은 무조건 거리가 0

    while (!heap.isEmpty()) { // heap이 비어있지 않다면
        // cost가 가장 낮은 정점을 뽑는다.
        const { node: current, cost: currentCost } = heap.pop();

        for (const [src, dest, cost] of road) { // 루프를 돌며 시작점, 도착점, 비용을 꺼낸다
            const nextCost = cost + currentCost; // 비용

            // 양방향을 고려하여 작성
            if (src === current && nextCost < dist[dest]) {
                // src가 현재 선택된 정점이면서 목적지까지 더 저렴할 경우
                dist[dest] = nextCost; // 거리를 갱신한다.
                heap.push({ node: dest, cost: nextCost }); // push
            } else if (dest == current && nextCost < dist[src]) {
                // dest가 현재 선택된 정점이면서 목적지까지 더 저렴할 경우
                dist[src] = nextCost; // 거리를 갱신한다.
                heap.push({ node: src, cost: nextCost }); // push
            }
        }
    }

    return dist; // 1번 마을부터 각 마을까지의 최단 거리
}


function solution(N, road, K) {
    const dist = dijkstra(road, N);
    return dist.filter(x => x <= K).length;
}
~~~ -->
