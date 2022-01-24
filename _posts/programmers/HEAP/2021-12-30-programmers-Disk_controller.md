---
layout: post
current: post
cover:  assets/built/images/programmers_logo.jpg
navigation: True
title: 프로그래머스 - 디스크 컨트롤러(Heap)
date: 2021-12-15 12:40:00
tags: [programmers, heap]
class: post-template
subclass: 'post tag-python'
author: sanghyoson
---
<i class="fa fa-search">&nbsp;</i> 
<a href='https://programmers.co.kr/learn/courses/30/lessons/42627'> Heap - 디스크 컨트롤러</a>
![프로그래머스 사진](../assets/built/images/programmers_logo.jpg){: width="100%" height="100%"}

<h2>문제 설명</h2>
<br/>
하드디스크는 한 번에 하나의 작업만 수행할 수 있습니다. 디스크 컨트롤러를 구현하는 방법은 여러 가지가 있습니다. 가장 일반적인 방법은 요청이 들어온 순서대로 처리하는 것입니다.

예를들어
와 같은 요청이 들어왔습니다. 이를 그림으로 표현하면 아래와 같습니다.
한 번에 하나의 요청만을 수행할 수 있기 때문에 각각의 작업을 요청받은 순서대로 처리하면 다음과 같이 처리 됩니다.
이 때 각 작업의 요청부터 종료까지 걸린 시간의 평균은 10ms(= (3 + 11 + 16) / 3)가 됩니다.

하지만 A → C → B 순서대로 처리하면
이렇게 A → C → B의 순서로 처리하면 각 작업의 요청부터 종료까지 걸린 시간의 평균은 9ms(= (3 + 7 + 17) / 3)가 됩니다.

각 작업에 대해 [작업이 요청되는 시점, 작업의 소요시간]을 담은 2차원 배열 jobs가 매개변수로 주어질 때, 작업의 요청부터 종료까지 걸린 시간의 평균을 가장 줄이는 방법으로 처리하면 평균이 얼마가 되는지 return 하도록 solution 함수를 작성해주세요. (단, 소수점 이하의 수는 버립니다)
<br/>

<h2>입력 형식</h2>
<ul class = 'data-contents'>
<br/>
<li>jobs의 길이는 1 이상 500 이하입니다.</li>
<li>jobs의 각 행은 하나의 작업에 대한 [작업이 요청되는 시점, 작업의 소요시간] 입니다.</li>
<li>각 작업에 대해 작업이 요청되는 시간은 0 이상 1,000 이하입니다.</li>
<li>각 작업에 대해 작업의 소요시간은 1 이상 1,000 이하입니다.</li>
<li>하드디스크가 작업을 수행하고 있지 않을 때에는 먼저 요청이 들어온 작업부터 처리합니다.</li>
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
어떻게 접근해야할지는 알겠으나,,, 구현을 하는 방법을 모르겠다 ... 뭐가 하나씩 부족하다 ㅠ.... 답답해 죽겠네 ..
최소 힙으로 접근해서 데이터를 처리할 수 있을 때, 최소힙으로부터 데이터를 뽑으면 된다... 그런데 안되네 ㅡㅡ
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
class MinHeap {
    constructor() {
        this.heap = [ null ];
    }
    
    size() {
        return this.heap.length - 1;
    }
    
    swap(a, b) {
        [ this.heap[a], this.heap[b] ] = [ this.heap[b], this.heap[a] ];
    }
    
    heappush(value) {
        this.heap.push(value);
        let curIdx = this.heap.length - 1;
        let parIdx = Math.floor(curIdx / 2);
        
        while(curIdx !== 0 && this.heap[parIdx] > this.heap[curIdx]) {
            this.swap(parIdx, curIdx)
            curIdx = parIdx;
            parIdx = Math.floor(curIdx / 2);
        }
    }
    
    heappop() {
        const min = this.heap[1];	
        if(this.heap.length <= 2) this.heap = [ null ];
        else this.heap[1] = this.heap.pop();   
        
        let curIdx = 1;
        let leftIdx = curIdx * 2;
        let rightIdx = curIdx * 2 + 1; 

        while(
            this.heap[leftIdx] < this.heap[curIdx] ||
            this.heap[rightIdx] < this.heap[curIdx]
        ) {
            const minIdx = this.heap[leftIdx] > this.heap[rightIdx] ? rightIdx : leftIdx;
            this.swap(minIdx, curIdx);
            curIdx = minIdx;
            leftIdx = curIdx * 2;
            rightIdx = curIdx * 2 + 1;
        }

        return min;
    }
}


function solution(jobs) {

  const heap = new MinHeap();
  
  const length = jobs.length;
  let answer = 0;
  let time = 0;

  jobs = jobs
    .sort((a, b) => a[0] - b[0])
    .map((v, i, arr) => [v[0] - arr[0][0], v[1]]);

  // 남은 작업이 있을 동안
  while (jobs.length || heap.size) {
    
    // 디스크의 현재 시간과 동일하거나 미리 요청된 작업이 존재한다면 heap에 추가한다. 
    // heap에 추가할 때마다 bubbleUp 방식으로 heapify를 실행한다.
    while (jobs.length && jobs[0][0] <= time) {
      heap.heappush(jobs.shift());
    }

    // 만약에 디스크의 현재 시간과 동일하거나 미리 요청된 작업이 없다면, 
    // 디스크의 현재 시간 이후에 요청된 작업이 존재하는지 확인해 heap에 추가한다.
    if (!heap.size) {
      const newTime = jobs[0][0];
      while (jobs.length && jobs[0][0] === newTime) {
        heap.heappush(jobs.shift());
      }
      
      // 디스크의 현재 시간을 새롭게 추가된 작업의 요청시간으로 갱신한다.
      time = newTime;
    }

    // 작업 대기열에서 가장 소요 시간이 짧은 작업을 꺼낸다. heap에서 꺼낼 때마다 bubbleDown 방식으로 heapify를 실행한다.
    const done = heap.heappop();
    
    // 현재 꺼낸 작업의 종료 시간을 더해 디스크의 현재 시간을 갱신한다.
    time += done[1];
    answer += time - done[0];
  }

  return Math.floor(answer / length);
}
~~~
