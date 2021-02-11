---
layout: post
title: "알고리즘 문제해결기법 입문 문제1I"
date: 2021-02-11
excerpt: "Python 알고리즘 문제해결기법 입문 문제1I"
tags: [Python, 알고리즘 문제해결기법 입문, Chapter.1]
comments: true
---
# 0A

### 문제
배운 내용을 바탕으로 선택 정렬을 구현해봅시다. 선택 정렬은 아래와 같은 연산을 반복하여 구현할 수 있습니다.

	1. 0번째 칸부터 (N-1)번째 칸 까지 데이터가 있는 배열에 아래의 과정을 수행한다
		1. 0~(N-1)번째 칸에서 최소값을 구하여 0번째 칸과 위치를 변경한다.
		2. 1~(N-1)번째 칸에서 최소값을 구하여 1번째 칸과 위치를 변경한다.
		3. ...
		4. (N-2)~(N-1)번째 칸에서 최소값을 구하여 (N-2)번째 칸과 위치를 변경한다.

### 입력 형식
첫 줄에 전체 데이터의 수 N이 주어진다. N은 1,000이하의 자연수이다.
두번째 줄에 32비트 정수형 데이터가 공백으로 구분되어 총 N개가 주어진다.

### 출력 형식
한 줄에 N개의 데이터를 오름차순으로 정렬하여 출력한다. 각 데이터는 하나의 공백으로 구분되어 있어야 한다.

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
선택정렬의 큰 토대는 selectionSort함수에서 이루어집니다. 해당 함수는 getMinIndexInRange함수에서 범위 내의 최소값의 인덱스를 받아와 현재 접근한 인덱스의 데이터와 자리를 바꿔주는 역할을 합니다. getMinIndexInRange함수의 범위는 현재 접근한 인덱스부터 마지막 인덱스까지 입니다. 값을 바꿔주는 것은 tmp를 이용하는 방법이 있지만 파이썬의 변수는 값을 가지고 있는 것이 아닌 참조하는 것이기 때문에 
{% highlight css %}
data[i], data[minIndex] = data[minIndex], data[i]
{% endhighlight %}
이 방법을 이용했습니다.
또, selectionSort는 data의 마지막까지 접근해서 수행할 이유가 없고 마지막-1까지만 접근을 하면 되기 때문에 시간 절약을 위해 selectionSort의 반복문의 종점을 n-1까지 설정해주었습니다.

### 코드
{% highlight css %}
def getMinIndexInRange(data, n, begin, end) :
	min_index = begin
	for i in range(begin + 1, end + 1) :
		if(data[min_index] > data[i]) : min_index = i
	return min_index

def selectionSort(data, n) :
	for i in range(n-1) :
		#주어진 범위에서 가장 작은 원소의 위치를 찾는다.
		minIndex = getMinIndexInRange(data, n, i, n-1);
		data[i], data[minIndex] = data[minIndex], data[i]
	return data

n = int(input())
data = list(map(int, input().split()))
for elem in selectionSort(data, n) :
	print(elem, end=' ')
{% endhighlight %}

### 기타
- `Memory` : 9460
- `Time` : 0.045