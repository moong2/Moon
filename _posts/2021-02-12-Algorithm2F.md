---
layout: post
title: "알고리즘 문제해결기법 입문 문제2F"
date: 2021-02-12
excerpt: "Python 알고리즘 문제해결기법 입문 문제2F"
tags: [Python, 알고리즘 문제해결기법 입문, Chapter.2]
comments: true
---
# 2F

### 문제
감수성이 풍부한 명은이는 매일 밤 하늘을 바라 본다. 어느 날 명은이는 태양을 중심으로 공전하는 지구와 또 그 지구를 중심으로 공전하는 달의 관계를 보며 깊은 고뇌에 빠졌다. 그 천체들은 계속 주위를 멤돌면서도 결국 일정거리 이상으로 가까워 질 수 없는 운명이기 때문이다. 명은이는 다음과 같은 생각을 하게 되었다.

> "지금 하늘에 떠 있는 천체들 중 서로 가장 가까이 있는 쌍은 무엇일까?"

감수성이라곤 찾아볼 수 없는, 뼛속까지 이과인 당신은 실제로 천체들간의 거리를 측정하여 가장 가까이 있는 두 천체를 명은이에게 알려주려고 한다. 가장 가까이 위치한 두 천체를 찾아보자.

### 입력 형식
첫 줄에는 하늘에 떠 있는 천체의 수 N이 주어진다. N은 2이상 1,000이하의 자연수이다.

그 후 총 N줄에 걸쳐서 각 줄에는 한 천체의 위치를 좌표로 나타내는 두 정수가 주어진다.

천체의 정보를 포함하는 N개의 각 줄에는 천체의 x좌표와 y좌표를 나타내는 두 정수가 공백으로 구분되어 주어진다. 모든 좌표는 절대값이 1만 이하인 정수이다. 모든 천체의 좌표는 서로 다르다.

### 출력 형식
첫 줄에는 가장 가까운 두 천체의 거리를 소수점 두 번째 자리에서 반올림하여 첫 번째 자리까지 출력한다.

두 번째 줄에는 그 거리만큼 떨어진 천체 쌍의 수를 출력한다.

### 예시 1
#### 입력
{% highlight css %}
2
1 1
2 2
{% endhighlight %}
#### 출력
{% highlight css %}
1.4
1
{% endhighlight %}

### 예시 2
#### 입력
{% highlight css %}
5
10000 9999
-10000 -9999
10000 -9999
-10000 9999
0 0
{% endhighlight %}
#### 출력
{% highlight css %}
14141.4
4
{% endhighlight %}

### 예시 3
#### 입력
{% highlight css %}
5
-1 5
2 5
3 2
3 6
-1 6
{% endhighlight %}
#### 출력
{% highlight css %}
1.0
1
{% endhighlight %}

# 풀이

### 설명
Class를 이용해서 x와 y좌표를 저장하고 관리하는 방법이 있지만 x와 y리스트를 따로 두고 딕셔너리에 계속해서 최소의 거리를 저장하는 방식으로 했습니다. 반복문은 마지막 인덱스를 빼고 전체적으로 한 바퀴를 돌고 안쪽 for문을 통해 해당 인덱스의 다음 인덱스부터 마지막 인덱스까지 돌며 거리를 구하는 방식을 이용했습니다. min_distance라는 변수를 두며 dict에는 key 하나만을 유지했습니다. min_distance의 최솟값은 가장 최대의 길이라고 생각되는 30000을 지정해주었습니다. 만일 현재 구한 distance가 min_distance와 같다면 해당 distance는 딕셔너리에 key로 저장이 되어있을 것이기에 value를 +1해주었습니다. distance가 min_distance보다 작다면 딕셔너리에 현재 저장되어 있는 key를 pop해주고 min_distance를 업데이트 하는 동시에 딕셔너리에 추가하여 value값을 1로 초기화했습니다.
시간복잡도는 O(N**2)입니다.

### 코드
{% highlight css %}
x_li = list()
y_li = list()
distance_di = dict()
min_distance = 30000
distance_di[min_distance] = 0

n = int(input())
for i in range(n) :
	x, y = map(int, input().split())
	x_li.append(x)
	y_li.append(y)

for i in range(n-1) :
	for j in range(i+1, n) :
		distance = round(((x_li[i] - x_li[j])**2 + (y_li[i] - y_li[j])**2)**0.5, 1)
		if(min_distance >= distance) :
			if(min_distance == distance) :	distance_di[min_distance] += 1
			else : 
				distance_di.pop(min_distance)
				min_distance = distance
				distance_di[min_distance] = 1
print(min_distance)
print(distance_di[min_distance])
{% endhighlight %}

### 기타
- `Memory` : 9771.6
- `Time` : 0.571