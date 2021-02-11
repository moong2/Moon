---
layout: post
title: "알고리즘 문제해결기법 입문 문제0D"
date: 2021-02-08
excerpt: "Python 알고리즘 문제해결기법 입문 문제0D"
tags: [Python, 알고리즘 문제해결기법 입문, Chapter.0]
comments: true
---
# 0A

### 문제
데이터의 수 N과 N개의 정수가 주어진다. 이 숫자들을 입력 순서와 정반대로 출력하는 프로그램을 작성하시오.

### 입력 형식
첫 줄에 데이터의 수를 나타내는 1이상 1,000이하의 자연수 N이 주어진다.
두 번째 줄에 공백으로 구분된 N개의 32비트 정수가 주어진다.

### 출력 형식
한 줄에 N개의 숫자들을 공백으로 구분하여 출력한다.

### 예시 1
#### 입력
{% highlight css %}
5
1 8 2 7 9
{% endhighlight %}
#### 출력
{% highlight css %}
9 7 2 8 1
{% endhighlight %}

### 예시 2
#### 입력
{% highlight css %}
3
72837 17263 9847
{% endhighlight %}
#### 출력
{% highlight css %}
9847 17263 72837
{% endhighlight %}

# 풀이

### 설명
파이썬의 기본 리스트를 활용해서 입력되는 숫자를 저장하고, 이를 반대로 출력하는 문제입니다. list는 map을 이용해 한번에 입력을 받았습니다. 또 반복문을 이용해 출력하는 방식과 join을 이용하는 방식 두 가지로 나눌 수 있었는데 반복문을 이용했습니다. 파이썬의 내장함수인 reversed()를 이용했고 반복문은 인덱스 접근이 아닌 요소 접근을 해서 풀었습니다.

### 코드
{% highlight css %} 
n = int(input())
arr = list(map(int, input().split()))
for elem in reversed(arr) : print(elem, end=' ')
{% endhighlight %}

### 기타
- `Memory` : 9525.3
- `Time` : 0.02