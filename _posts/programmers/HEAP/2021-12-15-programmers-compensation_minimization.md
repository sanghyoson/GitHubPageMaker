---
layout: post
current: post
cover:  assets/built/images/programmers_logo.jpg
navigation: True
title: 프로그래머스 - 배상 비용 최소화 실습(Heap)
date: 2021-12-15 12:40:00
tags: [programmers, heap]
class: post-template
subclass: 'post tag-python'
author: sanghyoson
---
<i class="fa fa-search">&nbsp;</i> 
<a href='https://programmers.co.kr/learn/courses/13213/lessons/91086'> Heap - 배상 비용 최소화 실습</a>
![프로그래머스 사진](../assets/built/images/programmers_logo.jpg){: width="100%" height="100%"}

<h2>문제 설명</h2>
<br/>
OO 조선소에서는 태풍으로 인한 작업지연으로 수주한 선박들을 기한 내에 완성하지 못할 것이 예상됩니다. 기한 내에 완성하지 못하면 손해 배상을 해야 하므로 남은 일의 작업량을 숫자로 매기고 배상비용을 최소화하는 방법을 찾으려고 합니다.
배상 비용은 각 선박의 완성까지 남은 일의 작업량을 제곱하여 모두 더한 값이 됩니다.

조선소에서는 1시간 동안 남은 일 중 하나를 골라 작업량 1만큼 처리할 수 있습니다. 조선소에서 작업할 수 있는 N 시간과 각 일에 대한 작업량이 담긴 배열(works)이 있을 때 배상 비용을 최소화한 결과를 반환하는 함수를 만들어 주세요. 예를 들어, N=4일 때, 선박별로 남은 일의 작업량이 works = [4, 3, 3]이라면 배상 비용을 최소화하기 위해 일을 한 결과는 [2, 2, 2]가 되고 배상 비용은 22 + 22 + 22 = 12가 되어 12를 반환해 줍니다.

<br/>

<h2>입력 형식</h2>
<ul class = 'data-contents'>
<br/>
<li>일할 수 있는 시간 N : 1,000,000 이하의 자연수</li>
<li>배열 works의 크기 : 1,000 이하의 자연수</li>
<li>각 일에 대한 작업량 : 1,000 이하의 자연수</li>
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
배상 비용이 남은시간의 제곱으로 발생되기 때문에, 총 비용을 최소화하기 위해서는 선박별 남은 작업량의 절대값들이 작아야한다. 따라서, 가장 큰 수를 작게 만드는 방향으로 접근한다.
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
function solution(no, works) {
    const heap = new MaxHeap();

    for (const work of works){
        heap.push(work);
    }
    
    for (let i = 0; i < no; i += 1){
        let mw = heap.pop();
        if (mw > 0){
            heap.push(mw-1);
        }
    }
    let answer = 0;
    
    for (let i = 1; i < heap.heap.length; i += 1){
        answer += heap.heap[i]**2
    }
    return answer;
}

class MaxHeap {
    constructor() {
        this.heap = [null];
    }
    
    push(val) {
        this.heap.push(val);
        let curInx = this.heap.length - 1;
        let parInx = Math.floor(curInx / 2);
        
        while (parInx !== 0 && this.heap[parInx] < val) {
            const tmp = this.heap[parInx];
            this.heap[parInx] = val;
            this.heap[curInx] = tmp;
            
            curInx = parInx;
            parInx = Math.floor(curInx / 2);
        }
    }
    
    pop() {
        const returVal = this.heap[1];
        if (this.heap.length > 2){
            this.heap[1] = this.heap.pop();
        } else {
            this.heap.pop();
        }
        
        let curInx = 1;
        let leftInx = 2;
        let rightInx = 3;
        
        while (
            this.heap[curInx] < this.heap[leftInx] ||
            this.heap[curInx] < this.heap[rightInx]
        ) {
            if (this.heap[leftInx] < this.heap[rightInx]) {
                const tmp = this.heap[curInx];
                this.heap[curInx] = this.heap[rightInx];
                this.heap[rightInx] = tmp;
                curInx = rightInx;
            } else {
                const tmp = this.heap[curInx];
                this.heap[curInx] = this.heap[leftInx];
                this.heap[leftInx] = tmp;
                curInx = leftInx;
            }
            leftInx = curInx * 2;
            rightInx = curInx * 2 + 1;
        }
        return returVal;
    }
}
~~~
