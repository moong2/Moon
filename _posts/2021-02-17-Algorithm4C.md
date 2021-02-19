---
layout: post
title: "알고리즘 문제해결기법 입문 문제4C"
date: 2021-02-17
excerpt: "Python 알고리즘 문제해결기법 입문 문제4C"
tags: [Python, 알고리즘 문제해결기법 입문, Chapter.4]
comments: true
---
# 4C

### 문제
두 자연수의 최대 공약수와 최소 공배수를 계산하는 프로그램을 작성해보자.

### 입력 형식
첫 줄에는 테스트케이스의 수 T가 1이상 100이하의 자연수로 주어진다.

이후 총 T줄에 걸쳐서 한 줄에 하나의 테스트케이스에 대한 입력이 주어진다.

- 각 테스트케이스의 입력은 한 줄에 두 자연수가 공백으로 구분되어 주어진다.
- 각 자연수는 1이상 10억이하의 자연수이다.

### 출력 형식
각 테스트케이스마다 두 줄에 걸쳐 결과를 출력한다.

- 각 테스트케이스의 첫 줄에는 테스트케이스의 번호를 Case #%d: 형식으로 출력한다. 대소문자와 공백에 주의한다.
- 두 번째 줄에는 최대 공약수와 최소 공배수를 공백으로 구분하여 순서대로 출력한다. 

### 예시 1
#### 입력
{% highlight css %}
3
24 18
1 1
9 3
{% endhighlight %}
#### 출력
{% highlight css %}
Case #1:
6 72
Case #2:
1 1
Case #3:
3 9
{% endhighlight %}

# 풀이

### 설명
유클리드 호제법을 이용해 문제를 풀었습니다. 유클리드 호제법은 최대공약수를 구하려는 두 수가 a, b일 때 a에 b를 대입하고 b에 a%b의 결과를 대입하며 a%b가 0이 아닐 때까지 계산을 반복합니다. 최소공배수는 gcd * (a / gcd) * (b / gcd) 이므로 정리를 하면 a * b / gcd가 됩니다. 

### 코드
{% highlight css %}
import sys

def getGCD(a, b) :
	result = 1
	while(a % b != 0) :
		result = a % b
		a = b
		b = result
	return b
def getLCM(a, b) :
	return a * b // getGCD(a, b)

t = int(input())
for i in range(t) :
	a, b = map(int, sys.stdin.readline().split())
	print(f'Case #{i+1}:')
	print(getGCD(a, b), getLCM(a, b))
{% endhighlight %}

### 기타
- `Memory` : 9445
- `Time` : 0.02