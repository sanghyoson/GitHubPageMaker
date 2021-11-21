---
layout: post
current: post
cover:  assets/built/images/programmers_logo.jpg
navigation: True
title: 추석 트래픽 - 알고리즘
date: 2021-11-04 12:40:00
tags: [algorithm, programmers]
class: post-template
subclass: 'post tag-python'
author: sanghyoson
---
<i class="fa fa-search">&nbsp;</i> 
<a href='https://programmers.co.kr/learn/courses/30/lessons/17676'> KAKAO 18\' RECRUITMENT - [1차] 추석 트래픽</a>
![프로그래머스 사진](../assets/built/images/programmers_logo.jpg){: width="100%" height="100%"}

<h2>문제 설명</h2>
<br/>
이번 추석에도 시스템 장애가 없는 명절을 보내고 싶은 어피치는 서버를 증설해야 할지 고민이다. 장애 대비용 서버 증설 여부를 결정하기 위해 작년 추석 기간인 9월 15일 로그 데이터를 분석한 후 초당 최대 처리량을 계산해보기로 했다. 초당 최대 처리량은 요청의 응답 완료 여부에 관계없이 임의 시간부터 1초(=1,000밀리초)간 처리하는 요청의 최대 개수를 의미한다.

<br/>

<h2>입력 형식</h2>
<ul class = 'data-contents'>
<br/>
<li>solution 함수에 전달되는 lines 배열은 N(1 ≦ N ≦ 2,000)개의 로그 문자열로 되어 있으며, 각 로그 문자열마다 요청에 대한 응답완료시간 S와 처리시간 T가 공백으로 구분되어 있다.</li>
<li>응답완료시간 S는 작년 추석인 2016년 9월 15일만 포함하여 고정 길이 2016-09-15 hh:mm:ss.sss 형식으로 되어 있다.</li>
<li>처리시간 T는 0.1s, 0.312s, 2s 와 같이 최대 소수점 셋째 자리까지 기록하며 뒤에는 초 단위를 의미하는 s로 끝난다.</li>
<li>예를 들어, 로그 문자열 2016-09-15 03:10:33.020 0.011s은 "2016년 9월 15일 오전 3시 10분 33.010초"부터 "2016년 9월 15일 오전 3시 10분 33.020초"까지 "0.011초" 동안 처리된 요청을 의미한다. (처리시간은 시작시간과 끝시간을 포함)</li>
<li>서버에는 타임아웃이 3초로 적용되어 있기 때문에 처리시간은 0.001 ≦ T ≦ 3.000이다.</li>
<li>lines 배열은 응답완료시간 S를 기준으로 오름차순 정렬되어 있다.</li>
</ul>
<br/>

<h2>출력 형식</h2>
<ul class = 'data-contents'>
<br/>
<li>solution 함수에서는 로그 데이터 lines 배열에 대해 초당 최대 처리량을 리턴한다.</li>
</ul>
<br/>

<h2>문제 풀이</h2>
<br/>
해당 문제는 크게 2가지 과정으로 해결하였다.
<ol class = 'data-contents'>
    <li>1. 문자열로부터 시작, 종료 시간 파싱하기</li>
    <li>2. 시간 포인트(시작, 종료시간)에서 오버랩되는 데이터의 수 카운트하기</li>
</ol>
<br/>

<h4>풀이과정 1 - 문자열로부터 시작, 종료 시간 파싱하기</h4>
<br/>
문자열로부터 원하는 숫자를 뽑아내는 파싱 과정 통해서 각 로그 데이터의 시작, 종료 시간을 구하는 것은 간단하다. 종료 시간에서 데이터 처리 시간을 빼면 시작 시간을 구할 수 있다. 다만, 해당 문제에서의 **핵심은 기본 환산단위를 ms로 변경**하는 과정인 것 같다.
문제 자체를 해결함에 있어서는 ms로의 환산이 크게 중요하지 않지만, 소수점으로 인해서 연산 중 오차가 발생하는 것을 확인하였다. (소수점 연산 속도 차이도 있을 것 같다.) 

<h4>풀이과정 2 - 시간 포인트(시작, 종료시간)에서 오버랩되는 데이터의 수 카운트하기</h4>
<br/>
초기 접근 방법은 1초간의 윈도우를 슬라이딩하며 각 윈도우에서 오버랩되는 데이터 수를 카운트하는 방법이었다. 해당 방법으로 원하는 결과를 얻을 수는 있지만, 효율성 측면에서 매우 떨어진다. 해당 **문제의 기본 시간 단위는 ms**이므로, 1초 동안 슬라이딩을 진행하여도 최소 1000번의 알고리즘이 진행되게 되고, 오버랩되는 카운터를 고려한다면 알고리즘 진행 시간은 더욱 늘어난다. 제안한 알고리즘의 **요청량이 변화하는 시점은 로그의 시작점, 종료점** 뿐이라는 점을 이용한다. 요청량이 변화는 전체 로그에서 시작, 종료점에서만 발생하므로, 해당 지점에서의 최대 요청량을 구하면, 전체 로그의 최대 요청량을 구할 수 있다. 따라서, 전체 시간을 슬라이딩 시키지 않고, 로그 시작, 종료점에서만 진행하여 구하였다.
<br/>


<h2>최종 코드</h2>
~~~javascript
function solution(lines) {
    let endTimes = [];
    let durations = [];
    let timeArr = [];
    let logPointArr = [];
    
    
    for (let i = 0; i < lines.length; i++){
        // data Parsing
        let splitWord = lines[i].split(/\s/);
        let splitEndTime = splitWord[1].split(':');
        let endTime = 3600 * Number(splitEndTime[0]) + 
            60 * Number(splitEndTime[1]) + Number(splitEndTime[2]);
        endTimes.push(endTime*1000);
        durations.push(1000*parseFloat(splitWord[2]));
        
        // get Array (start, end)
        let getTime = new Task(endTimes[i] - durations[i] + 1, endTimes[i]);
        timeArr.push([getTime.startTime,getTime.endTime]);
        logPointArr.push(getTime.startTime,getTime.endTime);
    }
    
    logPointArr.sort(function(a,b){return a-b})

    let max = 1;
    for (let i = 0; i < logPointArr.length; i++){
        let cnt = 0;
        for (let j = 0; j < timeArr.length; j++){
            checkOverLap(logPointArr[i], timeArr[j]) ? cnt ++ : 'none';
        }
        cnt > max ? max = cnt : 'none';
    }
    
    return max;
}

class Task {
    constructor(startTime, endTime)
    {
        this.startTime = startTime;
        this.endTime = endTime;
    }
    get startTime()
    {
        return parseInt(this._startTime);
    }

    set startTime(value)
    {
        this._startTime = value < 0 ? 0 : value;
    }
}

function checkOverLap(window, point){
    const windowStart = window;
    const windowEnd = window + 1000;
    const pointStart = point[0];
    const pointEnd = point[1];
    let result = false;
    
    if ((pointStart >= windowStart && pointStart < windowEnd) ||
        (pointEnd >= windowStart && pointEnd < windowEnd) ||
        (pointStart <= windowStart && pointEnd >= windowEnd))
        {
            result = true;
        }
    return result
}
~~~
