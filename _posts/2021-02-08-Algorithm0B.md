---
layout: post
title: "알고리즘 문제해결기법 입문 문제0B"
date: 2021-02-08
excerpt: "Python 알고리즘 문제해결기법 입문 문제0B"
tags: [Python, 알고리즘 문제해결기법 입문, Chapter.0]
comments: true
---
# 0A

#### 문제
표준입력 기능을 사용해 두 정수를 입력받고, 그 합을 출력하는 프로그램을 작성하시오.

#### 입력 형식
**한 줄에 공백으로 구분된** 두 정수가 입력된다.
- 두 정수와 그 합은 모두 32비트 정수형이라는 것이 보장된다.

#### 출력 형식
**두 정수를 더한 결과**를 한 줄에 공백없이 출력한다.

#### 예시 1
##### 입력
{% highlight css %}
3 8
{% endhighlight %}
##### 출력
{% highlight css %}
11
{% endhighlight %}

#### 예시 2
##### 입력
{% highlight css %}
-1 -1
{% endhighlight %}
##### 출력
{% highlight css %}
-2
{% endhighlight %}


# 풀이

#### 설명
한 줄에 두 int형 데이터를 입력받고 해당 데이터를 더해 출력합니다.
원래 사용하는 방법은
{% highlight css %}
a, b = map(int, input().split())
{% endhighlight %}
이었는데, 새로운 방법인
{% highlight css %}
a, b = [ int(w) for w in input().split()]
{% endhighlight %}
을 이용했습니다. 해당 문법은 for문으로 공백으로 구분된 str형 문자를 입력받고 그것을 int형으로 변환해 각 변수에 저장하는 역할을 합니다.

#### 코드
{% highlight css %}
#한 줄에 주어지는 두 정수를 a와 b에 저장하고 
a, b = [int(w) for w in input().split()]

#합을 구하여 answer에 저장하고
answer = a + b


#그 값을 출력한다
print(a + b)
{% endhighlight %}

#### 기타
- `Memory` : 9550.4
- `Time` : 0.034