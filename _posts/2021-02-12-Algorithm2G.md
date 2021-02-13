---
layout: post
title: "알고리즘 문제해결기법 입문 문제2G"
date: 2021-02-12
excerpt: "Python 알고리즘 문제해결기법 입문 문제2G"
tags: [Python, 알고리즘 문제해결기법 입문, Chapter.2]
comments: true
---
# 2G

### 문제
버블 정렬은 아래와 같은 알고리즘으로 동작합니다. 알고리즘을 이해해보고 직접 구현해봅시다.

	1. 데이터의 수를 N이라고 하자. 아래의 과정을 N번 반복한다.
		1. 배열의 0번 칸의 숫자가 1번 칸의 숫자 보다 크다면 두 값의 위치를 교환한다
		2. 배열의 1번 칸의 숫자가 2번 칸의 숫자 보다 크다면 두 값의 위치를 교환한다
		3. ...
		4. 배열의 N-2번 칸의 숫자가 N-1번 칸의 숫자 보다 크다면 두 값의 위치를 교환한다.

### 입력 형식
첫 줄에는 데이터의 수를 나타내는 자연수 N이 주어진다. N은 1이상 1,000이하의 자연수이다.

두 번째 줄에는 공백으로 구분된 N개의 정수가 주어진다. 모든 정수는 32비트 정수형 데이터이다.

### 출력 형식
한 줄에 N개의 오름차순으로 정렬 된 숫자들을 공백으로 구분하여 출력한다.

### 예시 1
#### 입력
{% highlight css %}
5
3 5 1 2 4
{% endhighlight %}
#### 출력
{% highlight css %}
1 2 3 4 5
{% endhighlight %}

# 풀이

### 설명
데이터를 리스트형식으로 입력을 받고 bubble_sort 함수에서 버블정렬을 수행했습니다. 시간복잡도는 O(N**2)입니다.

### 코드
{% highlight css %}
def bubble_sort(data) :
	for i in range(len(data) - 1) :
		for j in range(len(data) - 1 - i) :
			if(data[j] > data[j+1]) : data[j], data[j+1] = data[j+1], data[j]
	return data

n = int(input())
data_li = list(map(int, input().split()))
for elem in bubble_sort(data_li) :
	print(elem, end=' ')
{% endhighlight %}

### 기타
- `Memory` : 9534
- `Time` : 0.065