---
layout: post
title: "알고리즘 문제해결기법 입문 문제4I"
date: 2021-02-18
excerpt: "C++, Python 알고리즘 문제해결기법 입문 문제4I"
tags: [C++, Python, 알고리즘 문제해결기법 입문, Chapter.4]
comments: true
---
# 4I

### 문제
1742년에 독일의 수학자 골드바흐는 자신의 추측한 바를 정리하여 오일러에게 편지로 전했다. 골드 바흐의 추측은 아래와 같다.

> "4보다 큰 모든 짝수 자연수는 홀수인 두 소수의 합으로 표현될 수 있다."

아래와 같은 예시들에서 골드바흐의 추측이 성립한다.

8 = 3 + 5
20 = 3 + 17
42 = 5 + 37

당신은 실제로 골드바흐의 추측이 성립하는지 프로그램을 작성해 확인해보고자 한다. 여러 숫자가 주어질 때 그 숫자들에 골드바흐의 추측이 성립하는지 확인하는 프로그램을 작성하시오.

### 입력 형식
첫 줄에는 테스트케이스의 수 T가 주어진다. T는 100이하의 자연수이다.

테스트케이스의 각 줄에는 골드바흐의 추측이 성립하는지 확인해보고자 하는 6이상 백만이하의 자연수가 하나 주어진다.

### 출력 형식
각 테스트케이스마다 정답을 두 줄로 출력한다.

- 테스트케이스의 첫 줄에는 테스트케이스의 번호를 Case #%d: 형식으로 출력한다.
- 두 번째 줄에는 검증 결과를 출력한다.
	- 주어진 숫자에 대해 골드바흐의 추측이 성립했다면 해당 숫자와 두 홀수 소수를 x = a + b 형식으로 출력한다.
	- 성립하는 조합이 여러가지하면 a가 가장 작은 정답을 출력한다.
	- 성립하는 조합이 존재하지 않는다면 -1을 출력한다.

### 예시 1
#### 입력
{% highlight css %}
3
8
20
42
{% endhighlight %}
#### 출력
{% highlight css %}
Case #1:
8 = 3 + 5
Case #2:
20 = 3 + 17
Case #3:
42 = 5 + 37
{% endhighlight %}

# 풀이

### 설명
골드바흐의 추측은 두 개의 홀수의 소수의 합으로 모든 자연수를 나타낼 수 있다는 것이므로 에라토스테네스의 채 문제와 같은 방식을 이용하여 풀면 됩니다. 파이썬에서는 3번 케이스에서 시간초과가 나는 오류가 발생했는데 시스템 상 너무 적은 시간 제한을 두어 발생한 것으로 보입니다.

### 코드
{% highlight css %}
def find_prime(n) :
	sieve = [True] * (n+1)
	for i in range(3, int(n**0.5) + 1, 2) :
		if(sieve[i] == True) :
			for j in range(i+i, n+1, i) : sieve[j] = False
	return sieve

t = int(input())
for i in range(t) :
	x = int(input())
	print(f'Case #{i+1}:')
	prime_list = find_prime(x)
	g_conjecture = False
	for j in range(3, x//2+1, 2) :
		a = j
		b = x - a
		if(prime_list[a] and prime_list[b]) : 
			print(f'{x} = {a} + {b}')
			g_conjecture = True
			break
	if(g_conjecture == False) : print(-1)
{% endhighlight %}

### 기타
- `Memory` : 9636
- `Time` : 0.09