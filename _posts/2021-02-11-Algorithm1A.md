---
layout: post
title: "알고리즘 문제해결기법 입문 문제1A"
date: 2021-02-11
excerpt: "Python 알고리즘 문제해결기법 입문 문제1A"
tags: [Python, 알고리즘 문제해결기법 입문, Chapter.1]
comments: true
---
# 1A

### 문제
정수 두 개를 입력받아서 더 큰 값을 출력하는 프로그램을 작성하시오.

### 입력 형식
32비트 int형 정수 두 개가 공백으로 구분되어 한 줄에 주어진다.

### 출력 형식
두 정수 중 큰 정수를 한 줄에 공백없이 출력한다.

### 예시 1
#### 입력
{% highlight css %}
1 9
{% endhighlight %}
#### 출력
{% highlight css %}
9
{% endhighlight %}

# 풀이

### 설명
이미 기본 틀이 정해져 있고, 함수 내에서 큰 값을 반환하는 코드를 작성하면 되는 문제였습니다. 함수 내에서 else를 쓰지 않고 그냥 return b;만 해도 되지만 가독성을 위해 else를 사용했습니다.    

### 코드
{% highlight css %} 
#두 수중에 더 큰 값을 반환하는 함수
def get_max(a, b):
	#[begin]
	if(a > b) : return a;
	else : return b;
	#[end]
	
#두 값을 입력받는다 
p, q = map(int, input().split())
#더 큰 값을 answer에 저장한다
answer = get_max(p, q)
#한 줄에 답을 출력한다
print(answer)
{% endhighlight %}

### 기타
- `Memory` : 9342.8
- `Time` : 0.02