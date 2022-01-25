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

일단 JS에서 힙과 같은 데이터 구조를 제공하지 않는다 -> 구현을 해야하는데, 이것보다 더 간단하게 우선순위큐를 이용하여 해결 할 수 있다. 고정관념에서 벗어나야할듯 ...
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
function solution(jobs) {

    const heap = new MinHeap();

    const length = jobs.length;
    let answer = 0;
    let time = 0;

    jobs = jobs
        .sort((a, b) => a[0] - b[0]);
        // .map((v, i, arr) => [v[0] - arr[0][0], v[1]]);

    while (jobs.length > 0 || heap.size() > 0) {
        
        while (jobs.length > 0 && jobs[0][0] <= time) {
            let pop = jobs.shift()
            heap.heappush([pop[1], pop[0]]);
        }

        if (heap.size == 0) {
            const newTime = jobs[0][0];
            while (jobs.length > 0 && jobs[0][0] === newTime) {
                let pop = jobs.shift()
                heap.heappush([pop[1], pop[0]]);
            }

            time = newTime;
        }

        const done = heap.heappop();

        time += done[0];
        answer += time - done[1];
  }

  return Math.floor(answer / length);
}
~~~
<br/>
<br/>

<h2>참고 코드</h2>
~~~javascript
function solution(jobs) {
    var answer = 0;    
    
    // 우선 전체 작업 리스트를 요청시간의 오름차순으로 정렬한다.
    jobs.sort(function(a, b){
        return a[0] - b[0];
    });
    
    var now = 0;    // 작업이 완료된 현재 시간
    var total = 0;  // 대기 큐에서 우선순위가 낮은 첫번째 작업의 전체 작업시간
    var index = 0;  // 전체 작업 리스트 인덱스
    
    // 작업이 진행 중일 때 대기 큐    
    var priorityQueue = [];
    
    // 전체 작업 리스트를 모두 돌거나, 대기 큐 리스트가 있을 때 까지
    while( index < jobs.length || priorityQueue.length > 0 ){
        
        // 현재시간이 n번째 요청시간보다 크거나 같으면 대기 큐에 넣어준다.
        if( index < jobs.length && now >= jobs[index][0] ){
            
            // 대기 큐에 넣고 다음 작업으로 넘어간다.
            priorityQueue.push(jobs[index]);
            index = index + 1;
          
            // 대기 큐는 요청시간 순이 아닌 작업시간 오름차순으로 정렬한다.
            priorityQueue.sort(function(a, b){
                return a[1] - b[1];
            });
            
            continue;
        }
        
        if( !priorityQueue.length ){
            // 대기 큐가 없으면 현재시간을 첫번째 작업의 요청시간으로 세팅한다.
            now = jobs[index][0];
        }else{
            // 대기 큐가 있으면 첫번째 우선순위 작업의 전체시간을 계산한다.
            var data = priorityQueue.shift();            
            
            // 우선 대기큐가 끝났을 때의 현재시간을 계산 (ex: 3 - 9 - 18)
            now = now + data[1];
            
            // 현재 작업의 전체 소요시간 : 현재시간 - 요청시간 (ex : 3 - 7 - 17 )
            total = now - data[0];
            
            // 전체 요청시간을 누적
            answer = answer + total;
        }
    }
    // 누적된 전체 요청시간의 평균
    answer = parseInt(answer / jobs.length);
    return answer;
}
~~~
