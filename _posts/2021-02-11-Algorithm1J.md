---
layout: post
title: "알고리즘 문제해결기법 입문 문제1J"
date: 2021-02-11
excerpt: "Python 알고리즘 문제해결기법 입문 문제1J"
tags: [Python, 알고리즘 문제해결기법 입문, Chapter.1]
comments: true
---
# 0A

### 문제
평소 머리가 나쁘다고 놀림을 자주 듣는 예인이는 몰래 수학 공부를 하고 있다. 수학 공부를 하던 예인이는 자연수에 대한 깊은 고찰을 하게 되었다. 어떤 자연수 N이 있다고 했을 때 1이상 N 이하의 모든 자연수의 합은 손 쉽게 계산할 수 있다. 어떤 자연수 N이 있다고 했을 때, 아래와 같은 식의 값은 어떻게 계산할 수 있을까?



>(1이상 1이하의 모든 자연수의 합) + (1이상 2이하의 모든 자연수의 합) + ... +(1이상 N이하의 모든 자연수의 합)

 

어릴적부터 주술같은 주산을 배운 예인이는 위의 식을 계산하며 자신의 암산 능력을 다지기로 결정했다. 하지만 자신이 계산한 값이 정답이 맞는지 검증 할 수 없었던 예인이는 당신에게 자연수 N을 입력하면 위의 식으로 계산한 결과를 알려주는 프로그램을 요구했다. 컴퓨터를 잘 다룬다고 주변에 소문난 당신은 귀여운 예인이를 위하여 프로그램을 작성해주기로 결정하였다. 

### 입력 형식
첫 줄에 1이상 2,000이하의 자연수 N이 공백없이 주어진다.

### 출력 형식
첫 줄에 입력 값 N에 대하여 위의 식을 계산한 결과를 한 줄에 공백없이 출력한다.

### 예시 1
#### 입력
{% highlight css %}
100
{% endhighlight %}
#### 출력
{% highlight css %}
171700
{% endhighlight %}

# 풀이

### 설명
해당 문제는 간단하게 풀면 함수에서도 for문을 돌아야하고 함수 밖에서도 for문을 돌아야해서 O(n^^2)이 나오는 시간효율도가 좋지 않은 풀이방법이 나옵니다. 전 함수호출에서 나온 값을 저장해놨다가 해당 n만 더해 계속 저장한 것을 업데이트해나가는 식으로 풀이를 하면 더 빠를 것이라고 생각했습니다.

### 코드
#### O(N^^2)풀이
{% highlight css %}
def getRangeSumFromOne(n) :
	sum_all = 0
	for i in range(1, n+1) : sum_all += i
	return sum_all

n = int(input())
sum_all = 0
for i in range(1, n+1) : sum_all += getRangeSumFromOne(i)
print(sum_all)
{% endhighlight %}

#### O(N)풀이
{% highlight css %}
def getRangeSumFromOne(n) :
	global sum_stack
	sum_stack += n
	return sum_stack

n = int(input())
sum_stack = 0
sum_all = 0
for i in range(1, n+1) : sum_all += getRangeSumFromOne(i)
print(sum_all)
{% endhighlight %}

### 기타
#### O(N^^2) 풀이
- `Memory` : 9380.4
- `Time` : 0.1

#### O(N) 풀이
- `Memory` : 9274.8
- `Time` : 0.02