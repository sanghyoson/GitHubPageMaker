---
layout: post
current: post
cover:  assets/built/images/programmers_logo.jpg
navigation: True
title: 프로그래머스 - 단어 변환(BFS, DFS)
date: 2021-12-28 12:40:00
tags: [programmers, dfs bfs]
class: post-template
subclass: 'post tag-python'
author: sanghyoson
---
<i class="fa fa-search">&nbsp;</i> 
<a href='https://programmers.co.kr/learn/courses/30/lessons/43163?language=javascript'> BFS, DFS - 네트워크</a>
![프로그래머스 사진](../assets/built/images/programmers_logo.jpg){: width="100%" height="100%"}

<h2>문제 설명</h2>
<br/>
두 개의 단어 begin, target과 단어의 집합 words가 있습니다. 아래와 같은 규칙을 이용하여 begin에서 target으로 변환하는 가장 짧은 변환 과정을 찾으려고 합니다.
예를 들어 begin이 "hit", target가 "cog", words가 ["hot","dot","dog","lot","log","cog"]라면 "hit" -> "hot" -> "dot" -> "dog" -> "cog"와 같이 4단계를 거쳐 변환할 수 있습니다.

두 개의 단어 begin, target과 단어의 집합 words가 매개변수로 주어질 때, 최소 몇 단계의 과정을 거쳐 begin을 target으로 변환할 수 있는지 return 하도록 solution 함수를 작성해주세요.
<br/>

<h2>입력 형식</h2>
<ul class = 'data-contents'>
<br/>
<li>각 단어는 알파벳 소문자로만 이루어져 있습니다.</li>
<li>각 단어의 길이는 3 이상 10 이하이며 모든 단어의 길이는 같습니다.</li>
<li>words에는 3개 이상 50개 이하의 단어가 있으며 중복되는 단어는 없습니다.</li>
<li>begin과 target은 같지 않습니다.</li>
<li>변환할 수 없는 경우에는 0를 return 합니다.</li>
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
큐, 스택과 BFS를 적절히 활용. BFS를 이용하여 Target값이 존재하면 해당 값을 Return

<!-- <ol class = 'data-contents'>
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
function solution(begin, target, words) {
    let answer = -1;
    if (!(words.includes(target))) return 0;
    
    let q = new Queue();
    q.eq([begin, 0]);
    
    while (q.data().length > 0){
        let [cur_word, step] = q.dq();
        
        for (const word of words){
            let diff = 0;
            for (let i = 0; i < word.length; i++){
                if (word[i] !== cur_word[i]) diff += 1;
            }
            if ((diff == 1) && (word == target)) {
                step +=1;
                return step;
            } else if (diff == 1){
                q.eq([word, step+1]);
            }
        }
        
    }

    return answer;
}

class Queue{
    constructor(){
        this.q = [];
        this.f = 0;
        this.r = 0;
    }
    
    eq(val){
        this.q[this.r++] = val;
    }
    
    dq(){
        const val = this.q[this.f];
        delete this.q[this.f];
        this.f ++;
        return val;
    }
    
    data(){
        return this.q.slice(this.f,this.r);
    }
}
~~~
