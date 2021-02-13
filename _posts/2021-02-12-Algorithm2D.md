---
layout: post
title: "알고리즘 문제해결기법 입문 문제2D"
date: 2021-02-12
excerpt: "Python 알고리즘 문제해결기법 입문 문제2D"
tags: [Python, 알고리즘 문제해결기법 입문, Chapter.2]
comments: true
---
# 2D

### 문제
두 문자열을 사전순으로 비교하는 함수를 작성해봅시다.
- 언어의 string타입에 내장된 비교 기능을 사용하지 말고 직접 구현해보자.

### 입력 형식
한 줄에 하나씩 공백없이 영어 소문자로 구성된 문자열이 두 개 주어진다. 문자열의 길이는 10만 글자를 넘지 않는다.

### 출력 형식
두 문자열을 사전 순으로 비교한 결과에 따라서 아래와 같이 출력한다.

- 첫 줄에 입력된 문자열이 사전순으로 앞서는 문자열이라면 -1을 출력한다.
- 두 번째 줄에 입력된 문자열이 사전으로 앞서는 문자열이라면 1을 출력한다.
- 두 문자열이 일치한다면 0을 출력한다. 

### 예시 1
#### 입력
{% highlight css %}
algorithm
allergy
{% endhighlight %}
#### 출력
{% highlight css %}
-1
{% endhighlight %}

### 예시 2
#### 입력
{% highlight css %}
algorithm
algorithm
{% endhighlight %}
#### 출력
{% highlight css %}
0
{% endhighlight %}

### 예시 3
#### 입력
{% highlight css %}
allergy
algorithm
{% endhighlight %}
#### 출력
{% highlight css %}
1
{% endhighlight %}

# 풀이

### 설명
파이썬의 기본 string 비교 방법을 이용하면 편하지만 사용을 하지 말라는 조건이 있었기 때문에 직접 for문을 돌며 구했습니다. 먼저 두 단어가 길이가 같을 수도 있거나, 다를 수도 있다는 점을 나누기 위해서 min_len이라는 변수에 길이가 짧은 단어의 길이를 저장시켰습니다. 단어의 길이는 다르나 유사한 단어에 대한 조건을 다루기 위해서 입니다. 그 예로는 
{% highlight css %}
algorithm
algorith
{% endhighlight %}
가 있습니다. 이런 경우를 따로 생각해주어야 했기 때문에 for문의 종점을 min_len으로 설정했습니다. 위의 유사한 단어같은 예시가 아니라면 for문에서 가지치기로 빠질 수 있습니다. 위의 유사한 단어 예시나 같은 단어일 경우에는 palindrome변수가 True로 설정되어 있어 if문에서 걸러주어야합니다. 단어의 길이가 같을 경우 같은 단어이므로 0을 출력하고 min_len이 무슨 단어의 len인지에 따라서 -1과 1을 출력합니다. 시간복잡도는 O(N)입니다.

### 코드
{% highlight css %}
str1 = input()
str2 = input()
palindrome = True
if(len(str1) < len(str2)) : min_len = len(str1)
else : min_len = len(str2)
	
for i in range(min_len) :
	if(str1[i] > str2[i]) : 
		print(1)
		palindrome = False
		break
	elif(str1[i] < str2[i]) :
		print(-1)
		palindrome = False
		break
if(palindrome == True) : 
	if(len(str1) == len(str2)) : print(0)
	else :
		if(min_len == len(str1)) : print(-1)
		elif(min_len == len(str2)) : print(1)
{% endhighlight %}

### 기타
- `Memory` : 9428.8
- `Time` : 0.024