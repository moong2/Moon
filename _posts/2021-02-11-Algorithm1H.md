---
layout: post
title: "알고리즘 문제해결기법 입문 문제1H"
date: 2021-02-11
excerpt: "Python 알고리즘 문제해결기법 입문 문제1H"
tags: [Python, 알고리즘 문제해결기법 입문, Chapter.1]
comments: true
---
# 0A

### 문제
데이터 마이닝 과목을 수강하게 된 지애는 평소 수학과 컴퓨터와는 거리가 먼 삶을 살아왔기 때문에 과제에 애를 먹고있다. 평소 지애 괴롭히기를 좋아하는 미주는 진지하게 휴학을 고민하는 지애가 학교를 떠나는 것을 원하지 않기에 과제를 대신 해주기로 했다. 하지만 미주도 프로그래밍을 전혀 할 줄 모르기 때문에 평소 컴퓨터를 잘 다루기로 소문난 선배인 당신에게 과제를 부탁했다. 당신은 미주를 위하여 프로그램을 작성해야 한다.
N개의 수치 데이터가 정수로 주어진다. 당신은 이 개별 데이터들 중 전체 데이터의 평균과 가장 가까운 데이터와 그 번호를 출력하고자 한다. 가깝다라는 의미는 평균에서 그 숫자를 뺀 절댓값이 작다는 의미이다. 평균과의 거리가 같은 숫자가 두 개 이상일 경우, 가장 먼저 입력된 데이터를 우선으로 한다. 데이터의 번호는 입력받은 순서대로 1부터 N으로 부여된다.

### 입력 형식
첫 줄에 전체 데이터의 수 N이 10,000이하의 자연수로 주어진다.
두 번째 줄에는 각 수치 데이터가 공백으로 구분되어 한 줄에 주어진다. 각 수치 데이터는 -100,000 이상 100,000 이하의 정수이다.

### 출력 형식
한 줄에 평균과 가장 거리가 가까운 데이터의 번호와 그 값을 공백으로 구분하여 출력한다.

### 예시 1
#### 입력
{% highlight css %}
6
1 2 4 7 10 15
{% endhighlight %}
#### 출력
{% highlight css %}
4 7
{% endhighlight %}

# 풀이

### 설명
가장 핵심이라고 생각하는 계산 방법인 abs를 이용했습니다. abs는 해당 값의 절댓값을 리턴합니다. 모든 계산은 abs(평균 - 데이터의 값)을 이용을 했습니다. 변수는 abs가 가장 작았던 인덱스를 저장하는 min_sub_index와 가장 작은 abs를 저장하는 min_sub을 사용했습니다. 반복문에서 min_sub_index와 min_sub을 초기화시켜주기 위해 i가 0일 때를 특수조건으로 설정을 했는데 시간을 아끼기 위해서 min_sub_index와 min_sub을 선언할 때 먼저 계산을 했어도 되었을 것 같습니다. 초기화를 하고 난 뒤에는 sub이라는 변수에 해당 인덱스의 데이터와 평균의 차의 절댓값을 저장했고 이 sub이 min_sub보다 작을 경우에만 min_sub_index와 min_sub변수를 업데이트 해 주었습니다. 이는 차가 같을 경우 먼저 들어간 값을 저장하기 위한 방법입니다. 그리고 출력을 할 때, 인덱스 출력이 0부터 시작이 아니라 1이 시점이므로 min_sub_index+1을 출력을 하였고, min_sub_index로 data에 접근을 해서 출력을 했습니다.

### 코드
{% highlight css %}
n = int(input())
data = list(map(int, input().split()))
average = sum(data) / n
min_sub_index = -1
min_sub = -1
for i in range(len(data)) :
	if(i == 0) : 
		min_sub_index = i
		min_sub = abs(average - data[i])
	else : 
		sub = abs(average - data[i])
		if(sub < min_sub) :
			min_sub_index = i
			min_sub = sub
print(min_sub_index+1, data[min_sub_index])
{% endhighlight %}

### 기타
- `Memory` : 10235.2
- `Time` : 0.022