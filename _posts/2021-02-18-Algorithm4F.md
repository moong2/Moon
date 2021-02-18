---
layout: post
title: "알고리즘 문제해결기법 입문 문제4F"
date: 2021-02-18
excerpt: "C++, Python 알고리즘 문제해결기법 입문 문제4F"
tags: [C++, Python, 알고리즘 문제해결기법 입문, Chapter.4]
comments: true
---
# 4F

### 문제
주어진 범위에 존재하는 소수의 수를 출력하는 프로그램을 작성해보자.

### 입력 형식
첫 줄에는 테스트케이스의 수 T가 주어진다. T는 1이상 10이하의 자연수이다.

각 테스트케이스의 입력으로는 한 줄에 1이상 100만이하의 두 자연수 L과 R이 공백으로 구분되어 주어진다.

- L R 순서로 주어지며 L은 항상 R이하의 값이다.

### 출력 형식
각 테스트케이스에 대하여 두 줄씩 정답을 출력한다.

- 테스트케이스의 첫 줄에는 테스트케이스의 번호를 Case #%d: 형식으로 출력한다.
- 두 번째 줄에는 L이상 R이하의 소수의 갯수를 공백없이 출력한다.

### 예시 1
#### 입력
{% highlight css %}
3
2 10
50 100
100 1000
{% endhighlight %}
#### 출력
{% highlight css %}
Case #1:
4
Case #2:
10
Case #3:
143
{% endhighlight %}

# 풀이

### 설명
에라토스테네스의 채 알고리즘을 이용하면 쉽게 구할 수 있습니다. 해당 알고리즘은 find_prime함수에서 수행됩니다. 먼저, r+1만큼 sieve배열을 할당합니다. 이 배열은 True로 초기화되어 있습니다. r+1만큼 할당하는 이유는 l과 r이 1이 offset이기 때문입니다. 이 배열의 value가 True이면 해당 인덱스 숫자가 소수라는 것이고, False이면 소수가 아님을 나타냅니다. 소수를 판별하기 위해서 나누는 수는 2부터 r의 제곱수까지 입니다. 만약 해당 인덱스가 True이면 소수라는 것이므로 그 인덱스의 배수들을 모두 False로 바꾸어줍니다. 이 sieve배열에서 l과 r사이에 있는 값중 True인 것만 묶어 return을 하면 l과 r사이에 있는 소수를 모두 리턴할 수 있습니다. 처음에 2, 3번 케이스가 Fail이 떴는데 l이 1인 경우를 생각하지 않아서였습니다. sieve배열이 1일 때도 True로 설정되어 있는데 1은 소수가 아니므로 False로 바꾸어 줍니다. 

### 코드
{% highlight css %}
import sys

def find_prime(l, r) :
	sieve = [True] * (r+1)
	sieve[1] = [False]
	for i in range(2, int(r**0.5) + 1) :
		if (sieve[i] == True) :
			for j in range(i+i, r+1, i) :
				sieve[j] = False
	return [i for i in range(l, r+1) if sieve[i] == True]
	

t = int(input())
for i in range(t) :
	l, r = map(int, sys.stdin.readline().split())
	print(f'Case #{i+1}:')
	print(len(find_prime(l, r)))
{% endhighlight %}

### 기타
- `Memory` : 15381
- `Time` : 0.456