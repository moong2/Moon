---
layout: post
title: "알고리즘 문제해결기법 입문 문제0C"
date: 2021-02-08
excerpt: "Python 알고리즘 문제해결기법 입문 문제0C"
tags: [Python, 알고리즘 문제해결기법 입문, Chapter.0]
comments: true
---
# 0A

### 문제
주어진 숫자만큼 반복하여 Goorm를 출력하는 프로그램을 작성하시오.
각 단어 사이는 쉼표와 공백(<kbd>, </kbd>)으로 구분되어야 한다.
- 반복문과 조건문을 사용해 쉼표 출력 방법을 잘 설계하시오
- string join을 지원하는 언어는 이를 사용하면 편하다

### 입력 형식
첫 줄에 1이상 100이하의 자연수 N이 공백없이 주어진다.

### 출력 형식
N번에 걸쳐서 Goorm를 출력한다. 이 때, 각 텍스트 사이는 쉼표와 공백으로 구분된다.
- 출력 예시를 잘 확인하자

### 예시 1
#### 입력
{% highlight css %}
1
{% endhighlight %}
#### 출력
{% highlight css %}
Goorm
{% endhighlight %}

### 예시 2
#### 입력
{% highlight css %}
2
{% endhighlight %}
#### 출력
{% highlight css %}
Goorm, Goorm
{% endhighlight %}

### 예시 3
#### 입력
{% highlight css %}
3
{% endhighlight %}
#### 출력
{% highlight css %}
Goorm, Goorm, Goorm
{% endhighlight %}

### 예시 4
#### 입력
{% highlight css %}
10
{% endhighlight %}
#### 출력
{% highlight css %}
Goorm, Goorm, Goorm, Goorm, Goorm, Goorm, Goorm, Goorm, Goorm, Goorm
{% endhighlight %}

# 풀이

### 설명
반복문을 이용해서 Goorm사이에 <kbd>, </kbd>를 출력하는 방법을 이용하거나 join을 이용해 하나의 string을 만들어주는 방법을 이용하면 됩니다.
첫 Goorm의 앞뒤와 마지막 Goorm의 뒤에는 <kbd>, </kbd>가 존재하지 않는다는 점을 유의하며 풀었습니다.
a.join(b)에서 a는 문자열이고 b는 문자열의 배열을 의미합니다. b의 사이사이에 a를 끼워 넣어 하나의 str로 묶는 내장함수입니다. 그렇기에 반복문을 이용하는 것보다 메모리를 많이 사용합니다.

### 코드
#### 반복문
{% highlight css %} 
n = int(input())
for i in range(n) :
	if(i > 0) : print(", ", end='')
	print("Goorm", end='')
{% endhighlight %}

#### join
{% highlight css %}
n = int(input())
print(", ".join(["Goorm"]*n))
{% endhighlight %}

### 기타
#### 반복문
- `Memory` : 9428.6
- `Time` : 0.02

#### join
- `Memory` : 9527.4
- `Time` : 0.02