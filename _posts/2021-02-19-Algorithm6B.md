---
layout: post
title: "알고리즘 문제해결기법 입문 문제6B"
date: 2021-02-19
excerpt: "Python 알고리즘 문제해결기법 입문 문제6B"
tags: [Python, 알고리즘 문제해결기법 입문, Chapter.6]
comments: true
---
# 6B

### 문제
KOI 통신연구소는 레이저를 이용한 새로운 비밀 통신 시스템 개발을 위한 실험을 하고 있다. 실험을 위하여 일직선 위에 N개의 높이가 서로 다른 탑을 수평 직선의 왼쪽부터 오른쪽 방향으로 차례로 세우고, 각 탑의 꼭대기에 레이저 송신기를 설치하였다. 모든 탑의 레이저 송신기는 레이저 신호를 지표면과 평행하게 수평 직선의 왼쪽 방향으로 발사하고, 탑의 기둥 모두에는 레이저 신호를 수신하는 장치가 설치되어 있다. 하나의 탑에서 발사된 레이저 신호는 가장 먼저 만나는 단 하나의 탑에서만 수신이 가능하다. 

예를 들어 높이가 6, 9, 5, 7, 4인 다섯 개의 탑이 수평 직선에 일렬로 서 있고, 모든 탑에서는 주어진 탑 순서의 반대 방향(왼쪽 방향)으로 동시에 레이저 신호를 발사한다고 하자. 그러면, 높이가 4인 다섯 번째 탑에서 발사한 레이저 신호는 높이가 7인 네 번째 탑이 수신을 하고, 높이가 7인 네 번째 탑의 신호는 높이가 9인 두 번째 탑이, 높이가 5인 세 번째 탑의 신호도 높이가 9인 두 번째 탑이 수신을 한다. 높이가 9인 두 번째 탑과 높이가 6인 첫 번째 탑이 보낸 레이저 신호는 어떤 탑에서도 수신을 하지 못한다.

탑들의 개수 N과 탑들의 높이가 주어질 때, 각 각의 탑에서 발사한 레이저 신호를 어느 탑에서 수신하는지를 알아내는 프로그램을 작성하라. 

### 입력 형식
첫째 줄에 탑의 수를 나타내는 정수 N이 주어진다. N은 1 이상 500,000 이하이다. 둘째 줄에는 N개의 탑들의 높이가 직선상에 놓인 순서대로 하나의 빈칸을 사이에 두고 주어진다. 탑들의 높이는 1 이상 100,000,000 이하의 정수이다. 

### 출력 형식
첫째 줄에 주어진 탑들의 순서대로 각각의 탑들에서 발사한 레이저 신호를 수신한 탑들의 번호를 하나의 빈칸을 사이에 두고 출력한다. 만약 레이저 신호를 수신하는 탑이 존재하지 않으면 0을 출력한다.

### 예시 1
#### 입력
{% highlight css %}
5
6 9 5 7 4
{% endhighlight %}
#### 출력
{% highlight css %}
0 0 2 2 4
{% endhighlight %}

# 풀이

### 설명
스택을 이용하는 문제입니다. 레이저 탑을 저장한 배열을 돌면서 만약 스택에 아무 정보도 없을 때 해당 탑은 송신해 줄 레이저 탑이 없기 때문에 0으로 설정합니다. 현재 스택에 저장되어 있는 레이저 탑이 배열에 있는 레이저 탑보다 키가 작을 때 스택에 있는 키가 더 작은 모든 탑들을 POP합니다. 이 때 스택에 탑이 남아있다면 이 탑이 현재 레이저 탑의 레이저를 수신해 줄 탑이라는 말이 됩니다. 그러므로 수신해 줄 탑의 인덱스를 레이저라는 배열에 저장해주면 됩니다. 처음에는 이 인덱스를 배열의 index 함수를 이용했지만 timeout이 떠서 스택에 저장할 때 부터 튜플을 이용해 인덱스를 같이 저장하고 바로 빼서 사용하는 방식으로 고쳤습니다. 

### 코드
{% highlight css %}
import sys

n = int(input())
top_list = list(map(int, sys.stdin.readline().split()))
top_stack = list()
laser = [0]*n
for i, elem in enumerate(top_list) :
	while(len(top_stack) != 0 and top_stack[-1][0] <= elem) : top_stack.pop()
	if(len(top_stack) == 0) : laser[i] = 0
	else : laser[i] = top_stack[-1][1] + 1
	top_stack.append((elem, i))
	
for elem in laser :
	print(elem, end=' ')
{% endhighlight %}

### 기타
- `Memory` : 41050	
- `Time` : 0.616