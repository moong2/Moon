---
layout: post
title: "알고리즘 문제해결기법 입문 문제4D"
date: 2021-02-17
excerpt: "C++, Python 알고리즘 문제해결기법 입문 문제4D"
tags: [C++, Python, 알고리즘 문제해결기법 입문, Chapter.4]
comments: true
---
# 4D

### 문제
1부터 시작해서 1씩 증가하다가 특정 숫자에 도달하면 다시 1로 돌아오는 수열을 순환 수열이라고 하자. 예를 들어서 5에 도달하면 다시 1로 돌아오는 순환 수열은 아래와 같다.

> 1, 2, 3, 4, 5, 1, 2, 3, 4, 5, 1, 2, 3, 4, 5, ... 

이때 순환 주기가 서로 다른 수열들도 언젠가는 다시 모두가 1이 되는 시점이 존재한다. 예를 들어서 순환 주기가 2와 3인 아래의 두 수열을 보자.

> 1, 2, 3, 1, 2, 3, 1, 2, 3, ... 

> 1, 2, 1, 2, 1, 2, 1, 2, 1, ...

위의 두 수열은 서로 다른 순환 주기를 가지고 있지만 7번째 숫자에서 다시 동시에 시작하는 부분이 등장하게 된다. 그렇다면 총 N개의 순환 수열이 존재한다고 할 때, 모든 수열이 다시 1부터 시작되는 위치는 몇 번째 원소일까?

### 입력 형식
첫 줄에는 순환 수열의 수를 나타내는 1이상 10이하의  N이 주어진다.

두 번째 줄에는 각 수열의 순환 주기를 나타내는 자연수 N개가 공백으로 구분되어 주어진다. 순환주기는 1이상 100이하의 자연수이다.

### 출력 형식
첫 번째 원소를 제외하고 그 이후 최초로 모든 수열이 1이 되는 원소의 번호를 자연수로 출력한다.

### 예시 1
#### 입력
{% highlight css %}
2
2 3
{% endhighlight %}
#### 출력
{% highlight css %}
7
{% endhighlight %}

# 풀이

### 설명
유클리드 호제법을 이용해 문제를 풀었습니다. 최소공배수를 이용하면 되는 문제인데 문제는 두 수의 최소공배수가 아니라 여러 수의 최소 공배수를 구해야 한다는 것입니다. 그래서 최소공배수를 저장하는 lcm변수를 따로 두어 lcm변수와 수열의 주기를 저장한 배열에서 하나씩 꺼내 lcm을 계산하고 lcm변수를 업데이트 해 주었습니다.

### 코드
{% highlight css %}
import sys

def getGCD(a, b) :
	while(a % b != 0) :
		result = a % b
		a = b
		b = result
	return b
def getLCM(a, b) :
	return a * b // getGCD(a, b)

n = int(input())
circulation = list(map(int, sys.stdin.readline().split()))
lcm = circulation[0]
for i in range(1, n) :
	lcm = getLCM(lcm, circulation[i])
print(lcm + 1)
{% endhighlight %}

### 기타
- `Memory` : 9479
- `Time` : 0.02