---
layout: post
current: post
cover:  assets/built/images/programmers_logo.jpg
navigation: True
title: 프로그래머스 - 방문 길이(DP)
date: 2021-11-07 15:40:00
tags: [programmers, dp]
class: post-template
subclass: 'post tag-python'
author: sanghyoson
---
<i class="fa fa-search">&nbsp;</i> 
<a href='https://programmers.co.kr/learn/courses/30/lessons/49994'> Dynamic Programming - 방문 길이</a>
![프로그래머스 사진](../assets/built/images/programmers_logo.jpg){: width="100%" height="100%"}

<h2>문제 설명</h2>
<br/>
게임 캐릭터를 4가지 명령어를 통해 움직이려 합니다. 명령어는 다음과 같습니다.
<ul class = 'data-contents'>
<li>U: 위쪽으로 한 칸 가기</li>
<li>D: 아래쪽으로 한 칸 가기</li>
<li>R: 오른쪽으로 한 칸 가기</li>
<li>L: 왼쪽으로 한 칸 가기</li>
</ul>
<br/>
캐릭터는 좌표평면의 (0, 0) 위치에서 시작합니다. 좌표평면의 경계는 왼쪽 위(-5, 5), 왼쪽 아래(-5, -5), 오른쪽 위(5, 5), 오른쪽 아래(5, -5)로 이루어져 있습니다. 예를 들어, "ULURRDLLU"로 명령했다면 이때, 우리는 게임 캐릭터가 지나간 길 중 캐릭터가 처음 걸어본 길의 길이를 구하려고 합니다. 예를 들어 위의 예시에서 게임 캐릭터가 움직인 길이는 9이지만, 캐릭터가 처음 걸어본 길의 길이는 7이 됩니다. (8, 9번 명령어에서 움직인 길은 2, 3번 명령어에서 이미 거쳐 간 길입니다) 단, 좌표평면의 경계를 넘어가는 명령어는 무시합니다. 이때 캐릭터가 처음 걸어본 길의 길이는 7이 됩니다.
명령어가 매개변수 dirs로 주어질 때, 게임 캐릭터가 처음 걸어본 길의 길이를 구하여 return 하는 solution 함수를 완성해 주세요.
<br/>
<br/>


<h2>제한 사항</h2>
<ul class = 'data-contents'>
<br/>
<li>dirs는 string형으로 주어지며, 'U', 'D', 'R', 'L' 이외에 문자는 주어지지 않습니다.</li>
<li>dirs의 길이는 500 이하의 자연수입니다.</li>
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
DP를 이용해서 접근했다. 방문했던 길을 기억하고 있고, 최종적으로 DP로 쌓은 경로 딕션너리 길이를 출력하면 된다. 문제에 언급이 없기 때문에 초기 접근은 방향성을 고려하지 않았다. **즉, 동일한 길을 가더라도, 방향이 다르면 다른 길이라고 생각하고 접근했다.** 이러한 방법으로 접근하기 위해서, 도착하는 포인트를 Key로 도착할 떄의 Action들을 Values로 갖는 딕셔너리 형태로 기억하도록 한다. 예로, 초기 위치 (0,0)에서 'U'라는 인풋을 받아 (0,1)이라는 점으로 이동하면, 딕셔너리에 (0,1) :  {**'U' : 1**, 'D' : 0, 'R' : 0, 'L' : 0} 형태로 데이터를 저장한다. 최종적으로 Diction 내의 1의 개수를 구하면 된다.
<br/>
<br/>



<h2>초기 코드</h2>
~~~python
def solution(dirs):
    dic = {(0,0) : {'U' : 0, 'D' : 0, 'R' : 0, 'L' : 0}}    
    cp = [0, 0]
    
    for i, di in enumerate(dirs):
        if di == 'U' and cp[1] < 5:
            cp[1] += 1
        elif di == 'D' and cp[1] > -5:
            cp[1] -= 1
        elif di == 'R' and cp[0] < 5:
            cp[0] += 1
        elif di == 'L' and cp[0] > -5:
            cp[0] -= 1
        
        if tuple(cp) not in dic:
            dic[tuple(cp)] = {'U' : 0, 'D' : 0, 'R' : 0, 'L' : 0}
        if dic[tuple(cp)][di] == 0:
            dic[tuple(cp)][di] += 1
    result = 0
    for p, vals in dic.items():
        for _, val in vals.items():
            result += val
    return result
~~~

<br/>
<h2>문제 풀이 수정</h2>
<br/>
위와 같은 코드로 진행시 오류가 발생하였다. 방향성을 독립적인 것이라고 고려하였기 때문이라, 방향과 관계없이 거쳐간 길을 DP를 이용하여 기록하도록 하였다. 조금은 지저분하지만, 초기 위치에서 다음 위치로 이동하였을 때(사실 다른 풀이들도 뭐 그렇게 깔끔해보이진 않았음...), 두 점 사이의 중점을 DP에 저장하는 방식으로 접근하였다. 효율성 체크는 확인하지 않고, 통과하였기에 추가적인 풀이는 생략.
<br/>
<br/>



<h2>최종 코드</h2>
~~~python
def solution(dirs):
    dic = {}    
    cp = [0, 0]
    
    for i, di in enumerate(dirs):
        if di == 'U' and cp[1] < 5:
            cp[1] += 1
            m = cp[0]
            n = cp[1] - 0.5
        elif di == 'D' and cp[1] > -5:
            cp[1] -= 1
            m = cp[0]
            n = cp[1] + 0.5
        elif di == 'R' and cp[0] < 5:
            cp[0] += 1
            m = cp[0] - 0.5
            n = cp[1]
        elif di == 'L' and cp[0] > -5:
            cp[0] -= 1
            m = cp[0] + 0.5
            n = cp[1]
        
        if (m,n) not in dic:
            dic[(m,n)] = 1
        
    return len(dic)
~~~