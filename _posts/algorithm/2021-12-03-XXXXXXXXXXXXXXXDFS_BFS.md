---
layout: post
current: post
cover:  assets/built/images/algorithm.jpg
navigation: True
title: DFS, BFS의 구현 - 깊이 우선 탐색, 너비 우선 탐색
date: 2021-12-03 12:40:00
tags: [algorithm]
class: post-template
subclass: 'post tag-python'
author: sanghyoson
---
<i class="fa fa-search">&nbsp;</i> 
<a href='https://namu.wiki/w/DFS'> DFS? </a>
<a href='https://namu.wiki/w/BFS'> BFS? </a>
![알고리즘 사진](../assets/built/images/algorithm.jpg){: width="100%" height="100%"}

<h2>DFS(Depth-First Search), BFS(Breadth-First Search)?</h2>
<br/>
DFS, BFS 모두 그래프 탐색의 종류로서 각각 깊이 우선 탐색, 너비 우선 탐색이라 불린다. 그래프 내의 **모든 노드(node)를 방문하기 위한 완전 탐색** 방법론이며, 가지는 이름에서 알 수 있듯, 깊이를 우선적으로 탐색하거나 너비를 우선적으로 탐색하는 방법론이다. 아래 그림을 통해서 좀 더 직관적으로 이해할 수 있다.

<h3>DFS</h3>
![DFS](../assets/built/images/DFS.gif){: width="45%" height="45%"}
<a href='https://developer-mac.tistory.com/64'> 출처 : https://developer-mac.tistory.com/64 </a>

<h3>BFS</h3>
![BFS](../assets/built/images/BFS.gif){: width="45%" height="45%"}
<a href='https://developer-mac.tistory.com/64'> 출처 : https://developer-mac.tistory.com/64 </a>


DFS, BFS 알고리즘의 구현은 각각 Stack과 Queue를 이용한다. 여기서 궁금한 점은 **어떠한 원리로 Stack과 Queue를 이용하였을 때, DFS, BFS를 구현 할 수 있는가**였다. 블로그, 유튜브를 통해서 DFS, BFS를 구현한 코드를 찾을 수는 있었지만, 이들이 동작하는 원리에 대해서 정리된 곳은 거의 찾지 못했는데, 우연히 발견한 한 블로그에서 정리된 내용이 매우 인상 깊어 여기서 정리한다. 

<h2>DFS, BFS 구현하기</h2>
<br/>
앞서 DFS와 BFS는 **스택**과 **큐**를 이용한다고 언급했다. 내용은 해당 <a href='https://jeinalog.tistory.com/18'> 블로그</a>를 참고하였다. 아래와 같은 간단한 트리를 통해 예를 들어보자.

<h3>DFS 순서</h3>
<br/>
A > B > E > C > F > H > I > J > D > G > K
<br/>
<br/>
해당 순서가 어떻게 나오는지가 궁금한 것이었다. 이는 알고르짐을 스택으로 구현했기 때문에 위와 같은 순서로 나오는 것인데, 왜 위와 같은 순서로 나오는지 알아보자.




조금 더 간단히 얘기하면, 어떠한 목적이 있고 이를 달성하기 위해서 거쳐야하는 과정이 존재하는데 이를 기술하는 것을 의미한다. 알고리즘 특성은 다음 조건들을 만족해야 한다.

<ul class = 'data-contents'>
<li>입력 : 자료가 외부에서 하나 이상 제공되어야 한다.</li>
<li>출력 : 알고리즘의 결과로 하나 이상의 값이 도출되어야 한다.</li>
<li>유한성 : 알고리즘이 일정 작업이 지나면 종료되어야 한다. </li>
<li>명확성 : 명확한 작업과, 각 단계마다 명확한 다음 단계를 가져야한다. </li>
<li>효율성 : 실용적이여야 하며, 효율성이 높은 알고리즘일수록 가지가 높다. </li>
</ul>
<br/>
시간의 복잡도의 개념이 필요한 이유는 위에서 나열한 알고리즘 특성들 중 효율성과 관련이 있다. 효율성에서 볼 수 있듯, 같은 문제를 해결하는 알고리즘은은 여러 개가 존재하지만, 둘 중 효율적인 알고리즘이 더욱 우수한 알고리즘이라 할 수 있다. 효율적인 알고리즘(컴퓨터의 성능, 언어 등의 다른 변수가 동일하다면)일수록 컴퓨터가 빠르게 실행할 수 있다. 한편, 여러 알고리즘 중 효율적인 알고리즘이 무엇인지를 판단하기 위한 기준이 필요한데, 이때 필요한 개념이 시간복잡도와 공간복잡도이다.


<br/>
<h2>시간복잡도</h2>
<br/>
일반적으로 알고리즘의 복잡도는 시간복잡도와 공간복잡도로 평가를 하지만, 시간복잡도를 더 중요하게 평가한다. 요즘 많은 하드웨어들의 발달로 대용량의 메모리를 사용하는 것이 허용되기 때문에 시간복잡도를 위주로 판단한다.

<h4>복잡도 표기법</h4>
<br/>
시간 복잡도를 표현하는 알고리즘 표기법은 다음 세가지가 존재한다. 
<br/>
<ul class = 'data-contents'>
    <li>최상(Best)의 경우 : 빅오메가(Big-Omega) 표기법</li>
    <li>최악(Worst)의 경우 : 빅오(Big-O) 표기법</li>
    <li>평균(Average)의 경우 : 빅세타(Big-theta) 표기법</li>
</ul>
<br/>
이 중 가장 일반적으로 판단하는 표기법은 최악의 경우로 판단하는 빅오 알고리즘이다. 동일한 알고리즘이라고 하더라도 입력에 따라서 도출되는 시간이 다르다.
따라서, 최상으로 판단하는 빅오메가의 경우는 의미없는 결과이며, 평균을 이용하는 빅세타의 경우에는 계산이 복잡하고, 알고리즘의 성능을 직접적으로 비교하기 쉽지 않다.

<br/>
<h4>빅오 표기법의 수학적 정의</h4>
<br/>
> n ≥ n<sub>o</sub>인 모든 n에 대해서 kg(n) ≥ f(n)인 양수 k, n<sub>o</sub>이 존재하면,  f(n)=O(g(n))이라고 표기한다.

![알고리즘 사진](../assets/built/images/time_complexity_bigo.png){: width="40%" height="40%"}

충분히 큰 입력값 n을 넣었을때, 실행시간(running time) f(n)은 최악의 경우에도 점근 상한선을 넘을 수 없다.

<br/>
<h4>빅오 표기법의 성능 차이</h4>
<ul class = 'data-contents'>
<br/>
    <li>Big(1) : 해결하는 과정이 하나인 성능 지표</li>
    <li>Big(logN) : 해결하는 과정이 입력 개수가 증가함에 따라 감소하는 성능 지표</li>
    <li>Big(N) : 해결 과정이 입력개수와 동일한 성능 지표</li>
    <li>Big(N<sup>2</sup>) : 해결 과정이 입력값의 제곱에 비례하는 성능 지표</li>
    <li>Big(2<sup>N</sup>) : 해결 과정이 입력의 지수승만큼 증가하는 성능 지표</li>
</ul>
<br/>