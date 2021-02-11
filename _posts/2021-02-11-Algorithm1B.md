---
layout: post
title: "알고리즘 문제해결기법 입문 문제1B"
date: 2021-02-11
excerpt: "Python 알고리즘 문제해결기법 입문 문제1B"
tags: [Python, 알고리즘 문제해결기법 입문, Chapter.1]
comments: true
---
# 0A

### 문제
32비트 int형 정수가 N개 주어진다. 이 때 N개의 정수 중 가장 큰 값을 출력하는 프로그램을 작성하시오.

### 입력 형식
첫 줄에 입력 받을 숫자의 수 N이 주어진다. N은 10,000이하의 자연수이다.
두 번째 줄에 N개의 정수가 공백으로 구분되어 주어진다.

### 출력 형식
N개의 숫자 중 가장 큰 숫자를 첫 줄에 공백없이 출력한다.

### 예시 1
#### 입력
{% highlight css %}
10
2 -1 5 7 3 1 -50 5 4 7
{% endhighlight %}
#### 출력
{% highlight css %}
7
{% endhighlight %}

# 풀이

### 설명
이미 기본 틀이 정해져 있고, 함수 내에서 큰 값을 반환하는 코드를 작성하면 되는 문제였습니다. 여러 개의 정수 중에 최댓값을 구하는 방법으로는 파이썬 내장함수인 <kbd>max</kbd>를 사용하는 방법과 반복문을 돌며 직접 비교하면서 구하는 방법이 있습니다. 그런데 내장함수는 map 오브젝트를 컨트롤 할 수 있지만 반복문으로 돌면서 map에 접근하는 것은 불가합니다. 그렇기 때문에 함수 내부에서 받은 map을 list로 형변환 해줄 수 밖에 없는데 그 과정에서 메모리 손실이 나는 것을 발견할 수 있었습니다.

### 코드
#### 내장함수
{% highlight css %} 
#배열(data)의 원소 중 가장 큰 정수를 반환하는 함수를 작성해보자
def get_max(data, n):
	# begin 
	return max(data);
	# end 


#데이터의 수를 입력받는다
n = int(input())
#데이터들을 입력받는다
data = map(int, input().split())
#배열의 최대값을 저장한다 
answer = get_max(data, n)
#답을 출력한다
print(answer)
{% endhighlight %}

#### 반복문
{% highlight css %}
#배열(data)의 원소 중 가장 큰 정수를 반환하는 함수를 작성해보자
def get_max(data, n):
	# begin 
	data = list(data)
	for i in range(n) :
		if(i == 0) : max_num = data[i]
		else :
			if(max_num < data[i]) : max_num = data[i]
	return max_num
	# end 


#데이터의 수를 입력받는다
n = int(input())
#데이터들을 입력받는다
data = map(int, input().split())
#배열의 최대값을 저장한다 
answer = get_max(data, n)
#답을 출력한다
print(answer)
{% endhighlight %}

### 기타
#### 내장함수
- `Memory` : 10011
- `Time` : 0.02

#### 반복문
- `Memory` : 10223
- `Time` : 0.02