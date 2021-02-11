---
layout: post
title: "알고리즘 문제해결기법 입문 문제1C"
date: 2021-02-11
excerpt: "Python 알고리즘 문제해결기법 입문 문제1C"
tags: [Python, 알고리즘 문제해결기법 입문, Chapter.1]
comments: true
---
# 0A

### 문제
그룹의 리더 역할을 맡고 있는 수정이는 교보문고 한복판에서 사라진 지수와 미주를 찾고 있습니다. 하지만 교보문고에는 사람이 너무 많아 지수와 미주를 찾기가 너무 힘듭니다. 초인적인 능력을 가진 수정이는 멀리서도 사람들의 키를 1cm단위로 정확히 알아낼 수 있습니다. 수정이는 자신의 능력을 활용하여 미주나 지수와 키가 같은 사람만을 쫓아가 확인하기로 하였습니다. 현재 교보문고에 있는 모든 사람들의 수와 수정이가 인식한 키가 주어집니다. 주어지는 미주와 지수의 키를 활용하여 수정이는 최대 몇 명의 사람을 확인해야 하는 지 계산하는 프로그램을 작성해주세요.

### 입력 형식
첫 줄에 세 자연수 N, M, S가 주어진다. 각각 교보문고에 있는 수정이를 제외한 사람의 수 N, 미주의 키 M, 지수의 키 S이다.
두 번째 줄에 N명의 사람들의 키가 공백으로 구분되어 자연수로 입력된다.
사람들의 수 N은 10,000이하의 자연수이며, 모든 사람들의 키는 1이상  300이하의 자연수이다. 

### 출력 형식
수정이가 미주와 지수를 찾기위해 확인해보아야 할 후보의 수를 출력한다. 첫 줄에 공백없이 정수로 출력하면 된다.

### 예시 1
#### 입력
{% highlight css %}
10 165 167
165 180 175 167 128 200 167 138 176 156
{% endhighlight %}
#### 출력
{% highlight css %}
3
{% endhighlight %}

# 풀이

### 설명
파이썬의 내장함수인 <kbd>count</kbd>와 반복문을 이용하는 방법이 있습니다. <kbd>max</kbd>와 해당 내장함수는 달리 map 오브젝트에서는 쓸 수 없어 반복문과 마찬가지로 data를 list로 형변환 해주어야 합니다. 처음 문제를 풀었을 때 60점을 받았는데 m과 s가 같을 때 경우를 생각하지 않아 오답처리가 되었습니다. 내장함수를 사용할 때 조건을 걸지 않고 그냥 사용해버리면 m과 s가 같을 때 이중으로 더해지기 때문에 오답이 나옵니다.

### 코드
#### 내장함수
{% highlight css %} 
#데이터 N, M, S을 입력받는다 
n, m, s = map(int, input().split())

#공백으로 구분된 N개의 정수(사람들의 키)를 입력받는다
data = map(int, input().split())

#사람들의 수를 셀 변수 count를 0으로 초기화한다
count = 0

#[BEGIN ]
#count 변수에 정답(조사해야 할 사람의 수)이 저장되도록 코드를 작성해보자
data = list(data)
if(m != s) : count = data.count(m) + data.count(s)
else : count = data.count(m)

#[END]


print(count)
{% endhighlight %}

#### 반복문
{% highlight css %}
#데이터 N, M, S을 입력받는다 
n, m, s = map(int, input().split())

#공백으로 구분된 N개의 정수(사람들의 키)를 입력받는다
data = map(int, input().split())

#사람들의 수를 셀 변수 count를 0으로 초기화한다
count = 0

#[BEGIN ]
#count 변수에 정답(조사해야 할 사람의 수)이 저장되도록 코드를 작성해보자
data = list(data)
for elem in data :
	if(elem == m or elem == s) : count += 1

#[END]


print(count)
{% endhighlight %}

### 기타
#### 내장함수
- `Memory` : 9804
- `Time` : 0.02

#### 반복문
- `Memory` : 9792
- `Time` : 0.02