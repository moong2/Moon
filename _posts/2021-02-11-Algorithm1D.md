---
layout: post
title: "알고리즘 문제해결기법 입문 문제1D"
date: 2021-02-11
excerpt: "Python 알고리즘 문제해결기법 입문 문제1D"
tags: [Python, 알고리즘 문제해결기법 입문, Chapter.1]
comments: true
---
# 0A

### 문제
정수가 N개 주어진다. 이 N개의 정수의 합을 출력하는 프로그램을 작성하시오.

### 입력 형식
첫 줄에 입력되는 데이터의 수 N이 공백없이 입력된다. N은 1이상 1,000이하의 자연수이다.
두 번째 줄에는 공백으로 구분된 N개의 정수가 주어진다. 모든 숫자와 그 숫자들의 합은 항상 32비트 정수형으로 표현가능하다.

### 출력 형식
첫 줄에 입력된 N개의 숫자의 합을 공백없이 출력한다.

### 예시 1
#### 입력
{% highlight css %}
1
5
{% endhighlight %}
#### 출력
{% highlight css %}
5
{% endhighlight %}

### 예시 2
#### 입력
{% highlight css %}
3
50 10 -5
{% endhighlight %}
#### 출력
{% highlight css %}
55
{% endhighlight %}

# 풀이

### 설명
파이썬의 내장함수인 <kbd>sum</kbd>과 반복문을 이용하는 방법이 있습니다. 해당문제에서는 합을 반환하는 변수의 이름을 내장함수와 중복되게 설정하여 오류가 발생하지만 연습을 위해 해당 변수의 이름을 sum_data로 바꾸어 코드를 작성했습니다. 반복문을 이용할 때는 map 오브젝트인 data를 list로 형변환시켰습니다.

### 코드
#### 내장함수
{% highlight css %} 
def get_sum(data, n):
	sum_data = 0
	# 배열의 원소의 합을 저장할 수 있도록 코드를 작성해보세요
	sum_data = sum(data)
	# ...
	return sum_data


n = int(input())
data = map(int, input().split())
answer = get_sum(data, n)
print(answer)
{% endhighlight %}

#### 반복문
{% highlight css %}
def get_sum(data, n):
	sum = 0
	# 배열의 원소의 합을 저장할 수 있도록 코드를 작성해보세요
	for elem in list(data) :
		sum += elem
	# ...
	return sum


n = int(input())
data = map(int, input().split())
answer = get_sum(data, n)
print(answer)
{% endhighlight %}

### 기타
#### 내장함수
- `Memory` : 9450
- `Time` : 0.02

#### 반복문
- `Memory` : 9452
- `Time` : 0.02