---
layout: post
title: "알고리즘 문제해결기법 입문 문제1F"
date: 2021-02-11
excerpt: "Python 알고리즘 문제해결기법 입문 문제1F"
tags: [Python, 알고리즘 문제해결기법 입문, Chapter.1]
comments: true
---
# 0A

### 문제
N개의 정수로 이루어진 배열과 찾고자 하는 값 M이 주어진다. 이 배열에서 M이 존재하는 인덱스를 출력하는 프로그램을 작성하시오.

### 입력 형식
첫 줄에는 두 자연수 N과 M이 주어진다. N은 1만 이하의 자연수이다.
두 번째 줄에는 N개의 서로 다른 자연수가 공백으로 구분되어 주어진다.
입력되는 모든 숫자와 M은 1이상 1,000이하의 자연수임이 보장된다.

### 출력 형식
한 줄에 입력된 배열에서 M이 존재하는 인덱스를 정수로 공백없이 출력한다. 인덱스는 0이상 N-1이하의 정수라고 가정한다. 찾고자 하는 값이 배열에 없다면 -1을 출력한다.

### 예시 1
#### 입력
{% highlight css %}
3 2
2 3 1
{% endhighlight %}
#### 출력
{% highlight css %}
0
{% endhighlight %}

### 예시 2
#### 입력
{% highlight css %}
10 4
10 7 2 6 3 1 88 27 35 85
{% endhighlight %}
#### 출력
{% highlight css %}
-1
{% endhighlight %}

# 풀이

### 설명
반복문으로 푸는 방법과 내장함수인 <kbd>index</kbd>를 이용하는 방법이 있는데 이미 형식이 반복문으로 정해져 있어서 반복문을 이용했습니다. 반복문의 종점이 len(arr)로 되어있는데 이를 이용하기 위해서는 arr이 배열 형식이어야 하므로 list로 형변환을 해주고 시작을 했습니다. 또, 해당 value를 찾았다면 더 이상 반복문을 돌지 않아도 되므로 시간을 절약하기 위해 break를 해 주었습니다.

### 코드
{% highlight css %}
def find_value(value, arr):
	index = -1
	arr = list(arr)
	for i in range(0, len(arr)):
		#[BEGIN]
		if(arr[i] == value) : 
			index = i
			break
		#[END]
	return index

n, m = map(int, input().split())
data = map(int, input().split())
answer = find_value(m, data)
print(answer)
{% endhighlight %}

### 기타
- `Memory` : 9421.6
- `Time` : 0.02