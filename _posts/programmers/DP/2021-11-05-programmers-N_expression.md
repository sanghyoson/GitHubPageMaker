---
layout: post
current: post
cover:  assets/built/images/programmers_logo.jpg
navigation: True
title: 프로그래머스 - N으로 표현(DP)
date: 2021-11-05 12:40:00
tags: [programmers, dp]
class: post-template
subclass: 'post tag-python'
author: sanghyoson
---
<i class="fa fa-search">&nbsp;</i> 
<a href='https://programmers.co.kr/learn/courses/30/lessons/42895'> Dynamic Programming - N으로 표현</a>
![프로그래머스 사진](../assets/built/images/programmers_logo.jpg){: width="100%" height="100%"}

<h2>문제 설명</h2>
<br/>
아래와 같이 5와 사칙연산만으로 12를 표현할 수 있습니다.

12 = 5 + 5 + (5 / 5) + (5 / 5)

12 = 55 / 5 + 5 / 5

12 = (55 + 5) / 5

5를 사용한 횟수는 각각 6,5,4 입니다. 그리고 **이중 가장 작은 경우는 4**입니다.
이처럼 숫자 N과 number가 주어질 때, N과 사칙연산만 사용해서 표현 할 수 있는 방법 중 N 사용횟수의 최솟값을 return 하도록 solution 함수를 작성하세요.

<br/>

<h2>입력 형식</h2>
<ul class = 'data-contents'>
<br/>
<li>N은 1 이상 9 이하입니다.</li>
<li>number는 1 이상 32,000 이하입니다.</li>
<li>수식에는 괄호와 사칙연산만 가능하며 나누기 연산에서 나머지는 무시합니다.</li>
<li>최솟값이 8보다 크면 -1을 return 합니다.</li>
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
N을 최소한으로 이용하여 number를 구해야 하는데, **동일한 개수의 N을 가지고 표현할 수 있는 수는 매우 많다**. 접근방법은 N의 개수를 늘려가며 표현할 수 있는 수를 빈틈없이 계산하고 이 값들 중에서 number가 포함되는지 확인하는 것이다.
<ol class = 'data-contents'>
    <li>1. n개의 N을 이용하여 구할 수 있는 수 나열</li>
    <li>2. 나열된 수 중 number가 존재하는 확인</li>
</ol>
<br/>

<h2>풀이과정</h2>
<br/>
N을 n개를 이용하여 표현할 수 있는 수는 다음과 같이 구할 수 있다.

>N을 1개 이용한 집합과 N을 n-1개 이용한 집합의 사칙연산 집합 + N을 2개 이용한 집합과 N을 n-2개 이용한 집합의 사칙연산 집합 ...(반복)

**n이 8이 될 때까지 반복하였을 때, 해당 집합에 number가 존재하는지 확인하면 된다.**


<br/>


<h2>최종 코드</h2>
~~~python
def solution(N, number):
    answer = -1
    
    if N == number:
        return 1
    
    dic = [[N]]
    for N_num in range(2, 9):
        tmp = []
        for i in range(0, int((N_num+1)/2)):
            elements_1 = dic[i]
            elements_2 = dic[-1-i]
            
            for val1 in elements_1:
                for val2 in elements_2:
                    tmp.append(val1 + val2) 
                    tmp.append(val1 * val2)
                    tmp.append(val1 - val2 if val1 - val2 >= 0 else 0)
                    tmp.append(val2 - val1 if val2 - val1 >= 0 else 0)
                    if val2 != 0:
                        tmp.append(int(val1 / val2))
                    if val1 != 0:
                        tmp.append(int(val2/ val1))
            
        tmp.append(int(str(N)*N_num))
        dic.append(list(set(tmp)))
        
        if number in dic[N_num-1]:
            return N_num
    return answer
~~~
