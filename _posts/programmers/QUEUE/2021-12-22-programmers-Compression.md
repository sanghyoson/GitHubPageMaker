---
layout: post
current: post
cover:  assets/built/images/programmers_logo.jpg
navigation: True
title: 프로그래머스 - 압축 (Queue, Stack)
date: 2021-12-22 16:40:00
tags: [programmers, queue, stack]
class: post-template
subclass: 'post tag-python'
author: sanghyoson
---
<i class="fa fa-search">&nbsp;</i> 
<a href='https://programmers.co.kr/learn/courses/30/lessons/17684'> Queue, Stack - 압축</a>
![프로그래머스 사진](../assets/built/images/programmers_logo.jpg){: width="100%" height="100%"}

<h2>문제 설명</h2>
<br/>
신입사원 어피치는 카카오톡으로 전송되는 메시지를 압축하여 전송 효율을 높이는 업무를 맡게 되었다. 메시지를 압축하더라도 전달되는 정보가 바뀌어서는 안 되므로, 압축 전의 정보를 완벽하게 복원 가능한 무손실 압축 알고리즘을 구현하기로 했다.

어피치는 여러 압축 알고리즘 중에서 성능이 좋고 구현이 간단한 LZW(Lempel–Ziv–Welch) 압축을 구현하기로 했다. LZW 압축은 1983년 발표된 알고리즘으로, 이미지 파일 포맷인 GIF 등 다양한 응용에서 사용되었다.

LZW 압축은 다음 과정을 거친다.
<ul class = 'data-contents'>
<li>1. 길이가 1인 모든 단어를 포함하도록 사전을 초기화한다.</li>
<li>2. 사전에서 현재 입력과 일치하는 가장 긴 문자열 w를 찾는다.</li>
<li>3. w에 해당하는 사전의 색인 번호를 출력하고, 입력에서 w를 제거한다.</li>
<li>4. 입력에서 처리되지 않은 다음 글자가 남아있다면(c), w+c에 해당하는 단어를 사전에 등록한다.</li>
<li>5. 입력단계 2로 돌아간다.</li>
</ul>


압축 알고리즘이 영문 대문자만 처리한다고 할 때, 사전은 다음과 같이 초기화된다. 사전의 색인 번호는 정수값으로 주어지며, 1부터 시작한다고 하자.
예를 들어 입력으로 **KAKAO**가 들어온다고 하자. 
<ul class = 'data-contents'>
<li>1. 현재 사전에는 KAKAO의 첫 글자 K는 등록되어 있으나, 두 번째 글자까지인 KA는 없으므로, 첫 글자 K에 해당하는 색인 번호 11을 출력하고, 다음 글자인 A를 포함한 KA를 사전에 27 번째로 등록한다.</li>
<li>2. 두 번째 글자 A는 사전에 있으나, 세 번째 글자까지인 AK는 사전에 없으므로, A의 색인 번호 1을 출력하고, AK를 사전에 28 번째로 등록한다.</li>
<li>3. 세 번째 글자에서 시작하는 KA가 사전에 있으므로, KA에 해당하는 색인 번호 27을 출력하고, 다음 글자 O를 포함한 KAO를 29 번째로 등록한다.</li>
<li>4. 마지막으로 처리되지 않은 글자 O에 해당하는 색인 번호 15를 출력한다.</li>
</ul>
이 과정을 거쳐 다섯 글자의 문장 KAKAO가 4개의 색인 번호 [11, 1, 27, 15]로 압축된다.
<br/>
<br/>

<h2>입력 형식</h2>
<ul class = 'data-contents'>
<br/>
<li>입력으로 영문 대문자로만 이뤄진 문자열 msg가 주어진다. msg의 길이는 1 글자 이상, 1000 글자 이하이다.</li>
</ul>
<br/>


<h2>출력 형식</h2>
<ul class = 'data-contents'>
<br/>
<li>주어진 문자열을 압축한 후의 사전 색인 번호를 배열로 출력하라.</li>
</ul>
<br/>

<h2>문제 풀이</h2>
<br/>
큐 스택을 이용하여 간단하게 해결할 수 있을 것이라 판단했으나, 인덱스가 하나씩 밀리는 상황이 발생하였다... 통과는 하였으나, 코드가 매우 지저분함 ㅠㅠ

무분별하게... 스택, 큐를 사용해서 그런 것 같음. 스택 큐를 사용할 때 데이터의 형태 손실(?)되기 떄문에 데이터를 처리하기 힘든경우가 발생한다 ..
<!-- <ol class = 'data-contents'>
    <li>1. 비트 연산과 진법연산을 통해서 이진법 계산</li>
    <li>2. 2진법 연산시 동일한 자리수를 갖도록 하기위해서 나머지 자리를 0으로 저장</li>
    <li>3. 정규식을 이용하여 1 -> #, 0 -> ' '로 변환</li>
</ol> -->
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


<h2>초기 코드</h2>
~~~javascript
function solution(msg) {
    let dic = {};
    let al = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'.split('').forEach((v,i)=> dic[v]=i+1);
    
    const q = new Queue();
    for (let c of msg){
        q.eq(c);
    }   // queue 생성

    let result = [];
    
    let length = Object.keys(dic).length;
    let find = q.dq();
    while (true){
        while (true){
             if (find in dic){
                 if (q.size() > 0){
                     find += q.dq();
                 } else {
                     result.push(dic[find.slice(0,find.length)])
                     length++;
                     dic[find] = length;
                     find = '';
                     break;
                 }
             } else {
                 result.push(dic[find.slice(0,find.length-1)])
                 length++;
                 dic[find] = length;
                 break;
             }
        }
        
        if (find == '') break;
        find = find[find.length-1];
    }
    
    return result;
}

class Queue{
    constructor() {
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
        this.f += 1;
        return val;
    }
    
    size(){
        return this.r - this.f;
    }
}
~~~

<br/>
<h2>최종 코드</h2>
~~~javascript
function solution(msg) {
    var answer = [];
    const dictionary = {};
    let al = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'.split('').forEach((v,i)=> dictionary[v]=i+1);

    let nextIndex = 27;

    for (let i = 0; i < msg.length; i += 1) {
        let str = msg[i];
        let index = dictionary[str];

        for (let j = i + 1; j < msg.length; j += 1) {
            str += msg[j];
            if (dictionary[str]) {
                index = dictionary[str];
                i++;
            } else {
                dictionary[str] = nextIndex++;
                break;
            }
        }

        answer.push(index);
    }

    return answer;
}
~~~

