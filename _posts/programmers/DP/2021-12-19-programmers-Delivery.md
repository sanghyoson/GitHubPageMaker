---
layout: post
current: post
cover:  assets/built/images/programmers_logo.jpg
navigation: True
title: 프로그래머스 - 단어 퍼즐 실습 (dp)
date: 2021-12-18 12:40:00
tags: [programmers, dp]
class: post-template
subclass: 'post tag-python'
author: sanghyoson
---
<i class="fa fa-search">&nbsp;</i> 
<a href='https://programmers.co.kr/learn/courses/13213/lessons/91430'> DP - 단어 퍼즐 실습</a>
![프로그래머스 사진](../assets/built/images/programmers_logo.jpg){: width="100%" height="100%"}

<h2>문제 설명</h2>
<br/>
단어 퍼즐은 주어진 단어 조각들을 이용해서 주어진 문장을 완성하는 퍼즐입니다. 이때, 주어진 각 단어 조각들은 각각 무한개씩 있다고 가정합니다. 예를 들어 주어진 단어 조각이 [“ba”, “na”, “n”, “a”]인 경우 "ba", "na", "n", "a" 단어 조각이 각각 무한개씩 있습니다. 이때, 만들어야 하는 문장이 “banana”라면 “ba”, “na”, “n”, “a”의 4개를 사용하여 문장을 완성할 수 있지만, “ba”, “na”, “na”의 3개만을 사용해도 “banana”를 완성할 수 있습니다. 사용 가능한 단어 조각들을 담고 있는 배열 strs와 완성해야 하는 문자열 t가 매개변수로 주어질 때, 주어진 문장을 완성하기 위해 사용해야 하는 단어조각 개수의 최솟값을 return 하도록 solution 함수를 완성해 주세요. 만약 주어진 문장을 완성하는 것이 불가능하면 -1을 return 하세요.
<br/>

<h2>입력 형식</h2>
<ul class = 'data-contents'>
<br/>
<li>strs는 사용 가능한 단어 조각들이 들어있는 배열로, 길이는 1 이상 100 이하입니다.</li>
<li>strs의 각 원소는 사용 가능한 단어조각들이 중복 없이 들어있습니다.</li>
<li>사용 가능한 단어 조각들은 문자열 형태이며, 모든 단어 조각의 길이는 1 이상 5 이하입니다.</li>
<li>t는 완성해야 하는 문자열이며 길이는 1 이상 20,000 이하입니다.</li>
<li>모든 문자열은 알파벳 소문자로만 이루어져 있습니다.</li>
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
초기의 아이디어는 메모이제이션을 활용하되, 완전탐색을 진행하는 것이다. 즉, strs에 존재하는 각 원소를 n개를 이용하여 구할 수 있는 n개의 수를 모두 구하고, 해당 문자가 t와 같을 때, 그때의 n을 반환하는 것이다. 허나 해당 아이디어에는 n의 상한을 제한하는 데 한계가 있다. 각 원소의 개수는 무한대이기 때문에 해당 원소들의 이용해서 만들어지는 문자열의 개수 역시 무한대이다. 만들어지지 않을 경우 -1을 반환해야하는 데 무리가 있다는 뜻이다. (작성하면서 생각해보니, 조금의 시간의 소모가 있긴하겠지만 문자열의 길이가 t보다 길어지는 순간이 발생함을 이용하면 될 것 같다.)
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

~~~


<h2>참조 코드</h2>
~~~javascript
function solution(strs, t) {
    // 편의를 위해 t의 길이 + 1만큼 배열을 만든다.
    const dp = Array.from({ length: t.length + 1 }, () => 0);
    // 문자열 검사를 빠르게 하기 위해서 문자열 리스트를 set으로 만든다.
    const strsSet = new Set(strs);

    // 1부터 문자열 길이 + 1까지 루프를 돈다.
    for (let i = 1; i < t.length + 1; i += 1) {
        // 일단 해당 문자열의 최솟값은 무한으로 설정한다.
        dp[i] = Infinity;
        // 문자열을 자르면서 단어 조각을 찾기 위해 루프를 돈다.
        // 단어 조각은 5 이하기 때문에 마지막까지 자를 필요는 없다.
        for (let j = 1; j < Math.min(i + 1, 6); j += 1) {
            const start = i - j;
            const end = i;
            // 단어 조각이 있다면
            if (strsSet.has(t.slice(start, end))) {
                // 이전 조합과 더해서 최솟값인지 체크 후 대입한다.
                dp[i] = Math.min(dp[i], dp[i - j] + 1);
            }
        }
    }

    // 결과적으로 단어의 최솟값을 구할 수 있다. 만약 무한이라면 불가능한 조합이기 때문에 -1을 리턴한다.
    return dp[dp.length - 1] === Infinity ? -1 : dp[dp.length - 1];
}

~~~