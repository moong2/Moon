---
layout: post
title: "알고리즘 문제해결기법 입문 문제2C"
date: 2021-02-12
excerpt: "Python 알고리즘 문제해결기법 입문 문제2C"
tags: [Python, 알고리즘 문제해결기법 입문, Chapter.2]
comments: true
---
# 2C

### 문제
가수의 앨범은 팬들에게는 중요한 존재이다. 긴 기다림의 끝에 마주친 오아시스 같은 존재이기 때문이다. 그렇기에 최근의 가수들은 자신의 앨범에 기념품이나 손편지 등을 추가하여 팬들에게 고마운 마음을 전하고있다. 

인기 많은 아이돌 트와이스의 열렬한 팬인 민규는 이번에도 앨범을 사기 위하여 신촌의 한 백화점에 줄을 서서 대기하고있다. 이 백화점에서 판매하는 앨범은 한정판으로서, 각 앨범에는 임의의 화보가 한 장 들어있다. 이미 입대가 얼마남지 않은 민규는 자신의 모든 재산을 털어 트와이스 앨범을 구매하여 모든 종류의 화보를 수집하고자 한다.

각 화보들은 종류별로 고유한 번호를 가지고있으며 이 번호를 통해 같은 화보인지 아닌지 구분할 수 있다. 물론 여러 앨범들에는 같은 화보가 들어있을 수 있다. 민규는 총 N개의 앨범을 구매하여 화보들을 번호 순서대로 정렬하여 보관하려고 한다. 이 때 민규는 자신이 총 몇 종류의 화보를 획득하였는지 궁금해졌고, 코딩을 잘하는 당신에게 이를 계산하는 프로그램을 작성해주기를 부탁하였다. 민규의 마지막 소원을 들어주기 위하여 프로그램을 작성하시오.

### 입력 형식
첫 줄에는 화보의 수 N이 주어진다. N은 1이상 10만 이하의 자연수이다.

두 번째 줄에는 각 화보의 고유번호가 공백으로 구분되어 주어진다. 각 화보의 고유번호는 32비트 정수형 중 하나로 주어지며, N개의 고유번호는 오름차순으로 주어진다.

### 출력 형식
한 줄에 중복을 제외한 화보의 종류의 수를 공백없는 자연수로 출력한다. 

### 예시 1
#### 입력
{% highlight css %}
5
1 2 3 4 5
{% endhighlight %}
#### 출력
{% highlight css %}
5
{% endhighlight %}

### 예시 2
#### 입력
{% highlight css %}
5
1 2 3 4 4
{% endhighlight %}
#### 출력
{% highlight css %}
4
{% endhighlight %}

### 예시 3
#### 입력
{% highlight css %}
5
-1 -1 -1 -1 -1
{% endhighlight %}
#### 출력
{% highlight css %}
1
{% endhighlight %}

# 풀이

### 설명
화보의 고유번호를 받아 딕셔너리에 옮겨 저장하는 방법을 이용했습니다. 딕셔너리는 같은 Key값이 같으면 value값이 업데이트만 되기 때문에 딕셔너리에 옮기고 len값을 출력해주었습니다.

### 코드
{% highlight css %}
n = int(input())
unique_number_li = list(map(int, input().split()))
unique_number_di = dict()

for elem in unique_number_li :
	unique_number_di[elem] = 0

print(len(unique_number_di))
{% endhighlight %}

### 기타
- `Memory` : 15616
- `Time` : 0.037