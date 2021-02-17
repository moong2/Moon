---
layout: post
title: "알고리즘 문제해결기법 입문 문제4E"
date: 2021-02-17
excerpt: "C++, Python 알고리즘 문제해결기법 입문 문제4E"
tags: [C++, Python, 알고리즘 문제해결기법 입문, Chapter.4]
comments: true
---
# 4E

### 문제
자연수를 소인수 분해한 결과를 출력하는 프로그램을 작성해보자. 입력으로 주어진 자연수를 소인수분해 한 후 해당 숫자의 소인수들을 나열하면 된다.

### 입력 형식
첫 줄에는 테스트케이스의 수 T가 주어진다. T는 1이상 100이하의 자연수이다.

각 테스트케이스는 한 줄로 구성되며 소인수 분해를 할 자연수가 주어진다. 이 자연수는 2이상 10억이하이다. 

### 출력 형식
각 테스트케이스에 대한 정답을 두 줄씩 출력한다.

- 테스트케이스의 첫 줄에는 테스트케이스의 번호를 #%d: 와 같은 형식으로 출력한다.
- 두 번째 줄에는 입력으로 주어진 숫자들의 소인수들을 공백으로 구분하여 오름차순으로 출력한다. 여러 번 곱해진 소인수는 그 횟수 만큼 출력한다.

### 예시 1
#### 입력
{% highlight css %}
3
24
28
21
{% endhighlight %}
#### 출력
{% highlight css %}
#1:
2 2 2 3 
#2:
2 2 7 
#3:
3 7 
{% endhighlight %}

# 풀이

### 설명
자연수에 대한 소인수를 구하고, 여러 번 곱해진 소인수일 경우 그 횟수만큼 풀어서 출력하는 문제입니다. 딕셔너리로 소인수를 저장해서 value만큼 반복 출력하기도 했고, list안에 처음부터 계산되어져 나오는 소인수를 저장해 그대로 list를 출력하는 방식을 이용하기도 했습니다. 이 두 방법 모두에는 문제가 없지만 시간초과가 발생했는데 이는 factorization함수 내에 있는 반복문의 종점 때문입니다. n+1까지 반복문을 돌 경우 최대 반복문은 10억회를 돌아야 하기 때문에 시간 초과가 당연하게 발생합니다. 저는 처음에 n//2+1을 종점으로 두어 n//2까지 돌 수 있도록 하였는데 이렇게 하더라도 시간초과가 발생했습니다. 그래서 소수를 구할 때 n**0.5까지만 계산을 했던 아이디어에 착안하여 종점을 제곱수까지로 설정하였고, 반복문을 끝내고 나왔을 때 n이 1보다 크면 해당 n이 소수였다는 것을 의미하므로 딕셔너리 혹은 리스트에 추가를 하였습니다.

### 코드
{% highlight css %}
def factorization(n) :
	# prime_factor = list()
	prime_factor = dict()
	for i in range(2, int(n**0.5)+1) :
		prime_factor[i] = 0
		while (n % i == 0) :
			# prime_factor.append(i)
			prime_factor[i] += 1
			n //= i
		if(prime_factor[i] == 0) : del(prime_factor[i])
	if(n > 1) : prime_factor[n] = 1
	# if(n > 1) : prime_factor.append(n)
	return prime_factor

t = int(input())
for i in range(t) :
	n = int(input())
	print(f'#{i+1}:')
	# for elem in factorization(n) : print(elem, end=' ')
	for key, value in factorization(n).items() :
		for _ in range(value) : print(key, end=' ')
	print()
{% endhighlight %}

### 기타
- `Memory` : 9589
- `Time` : 0.183