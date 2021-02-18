---
layout: post
title: "알고리즘 문제해결기법 입문 문제4J"
date: 2021-02-18
excerpt: "C++, Python 알고리즘 문제해결기법 입문 문제4J"
tags: [C++, Python, 알고리즘 문제해결기법 입문, Chapter.4]
comments: true
---
# 4I

### 문제
평소 모든 게임을 다 잘하는 예인이는 게임의 여왕으로 불린다. 하지만 이번 MT에서 똑똑한 수정이가 준비한 게임은 수학적인 아이디어를 요구하기 때문에 애를 먹고 있다. 수정이가 준비한 게임은 아래와 같은 규칙으로 진행된다.

- 게임을 하는 참가자는 가장 먼저 자연수가 적힌 카드 N개를 받는다.
- 참가자는 자신이 원하는 횟수만큼 아래의 동작을 반복할 수 있다.
	- N개의 숫자들 중 두 개의 숫자 A와 B를 고르고 B의 약수 P를 하나 고른다.
	- 숫자 A가 적힌 카드를 반납하고 숫자 (A×P)가 적힌 카드를 가진다.
	- 숫자 B가 적힌 카드를 반납하고 숫자 (B÷P)가 적힌 카드를 가진다.
- 게임이 종료될 때 각 사람은 자신이 들고있는 카드들에 적힌 숫자들 전부의 최대공약수 만큼 점수를 획득한다.

예인이는 제한 시간동안 마구잡이로 여러 방법을 시도해보고 있지만, 자신이 얻은 점수가 높은 점수인지 확신을 할 수 가 없었다. 예인이를 도와서 처음에 주어진 숫자 카드를 통해 얻을 수 있는 최고의 점수를 계산하는 프로그램을 작성해주자.

### 입력 형식
첫 줄에는 처음에 주어지는 숫자 카드의 수 N이 주어진다. N은 1이상 100이하의 자연수이다. 

두 번째 줄에는 총 N개의 카드에 적혀있는 숫자가 주어진다. 처음 카드에 적혀있는 숫자는 100만이하의 자연수이다.

### 출력 형식
예인이가 얻을 수 있는 최대의 점수를 한 줄에 자연수로 출력한다.

### 예시 1
#### 입력
{% highlight css %}
3
4 4 1
{% endhighlight %}
#### 출력
{% highlight css %}
2
{% endhighlight %}

### 예시 2
#### 입력
{% highlight css %}
3
8 24 9
{% endhighlight %}
#### 출력
{% highlight css %}
12
{% endhighlight %}

# 풀이

### 설명
처음에는 문제 이해가 잘 되지 않았습니다. 해당 문제는 각각의 소인수를 다른 카드에 줄 수 있다는 개념이 전제인데 최대공약수가 최대일 때를 구하는 문제입니다. 최대공약수가 최대이면 N개의 카드의 인수가 골고루 분포되어 있어야 합니다. 그래서 저는 factorization함수에서 factorization_dict라는 딕셔너리에 각각의 인수와 그 개수의 합산을 저장하고 이를 이용했습니다. 각각의 인수를 골고루 분포시키기 위해서는 개수를 n으로 나누어야 합니다. 이 때 그 결과가 0이면 골고루 나눌 수 없다는 얘기가 되므로 곱하지 않습니다. 처음에 계속 fail이 떴는데 그 이유가 함수 내부에서 num>1일 경우에 무조건적으로 factorization_dict[num]을 1로 초기화해버리니까 정수가 7 14가 들어왔을 때 공약수인 7이 계속 1로 업데이트 되어 있었습니다. 이를 고치기 위해서 num>1일 때도 딕셔너리에 해당 키가 있는지 없는지를 판단하는 조건을 두었습니다.

### 코드
{% highlight css %}
import sys
factorization_dict = dict()
def factorization(num) :
	global factorization_dict
	for i in range(2, int(num**0.5) + 1) :
		if(i not in factorization_dict) : factorization_dict[i] = 0
		while (num % i == 0) :
			factorization_dict[i] += 1
			num //= i
		if(factorization_dict[i] == 0) : del(factorization_dict[i])
	if(num > 1) : 
		if(num in factorization_dict) : factorization_dict[num] += 1
		else : factorization_dict[num] = 1

n = int(input())
n_li = list(map(int, sys.stdin.readline().split()))
for elem in n_li :
	factorization(elem)
gcd = 1
for key,value in factorization_dict.items() :
	v = value//n
	if(v != 0) : gcd = gcd*(key**v)
if(gcd == 1) : gcd
print(gcd)
{% endhighlight %}

### 기타
- `Memory` : 9598
- `Time` : 0.0225