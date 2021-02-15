---
layout: post
title: "알고리즘 문제해결기법 입문 문제3G"
date: 2021-02-15
excerpt: "Python 알고리즘 문제해결기법 입문 문제3G"
tags: [Python, 알고리즘 문제해결기법 입문, Chapter.3]
comments: true
---
# 3F

### 문제
인기 아이돌 그룹 코들리즈(Codelyz)의 매니저인 당신은 우여곡절끝에 팬 사인회를 성공적으로 성공시켰다. 팬 카페에서도 이번 팬 사인회 선발 기준에 대한 긍정적인 반응들이 많았고, 회사에서도 당신의 문제해결능력을 칭찬하였다. 하지만 능력있는 사람은 항상 바쁜 법, 후배 매니저가 기획한 팬 사인회 내부 이벤트에 해결해야 할 문제가 있어 이를 도와주어야 한다. 후배 매니저가 기획한 이벤트는 아래와 같다.

- 팬 사인회에서 기본적으로 모든 팬들은 정해진 좌석에 앉아서 대기한다.
- 모든 좌석은 1부터 N번 사이의 자연수로 번호가 매겨져 있으며, 팬들은 좌석을 옮길 수 없다.
- 당신은 이 중 연속한 좌석 K개를 선택해 해당 좌석에 앉은 팬들을 대상으로 이벤트를 진행해야 한다.
- 이 이벤트는 생년월일 6자리를 사용한 추첨을 진행할 것이기 때문에, 이 K명끼리 서로 모두 주민등록번호 앞자리가 달라야만 한다.

각 팬들의 주민등록번호 앞자리가 숫자로 주어질 때, 당신은 이 이벤트를 진행할 수 있도록 연속한 K명을 선발할 수 있는 방법이 몇 가지인지 확인하고자 한다. 

예를 들어 N=5, K=2일 때 아래와 같이 팬들의 생년월일이 있다면, 총 3가지 경우의 수가 존재한다.
{% highlight css %}
	930503	930503	890412	670610	680525
{% endhighlight %}

### 입력 형식
첫 줄에는 팬의 수 N과 선발해야 할 사람의 수 K가 1이상 20만 이하의 자연수로 주어진다.

두 번째 줄에는 공백으로 구분 된 생년월일 6자리가 공백으로 구분되어 주어진다. 생년월일은 6자리 숫자로만 주어진다.

### 출력 형식
생년월일이 서로 다른 연속된 K명을 선발할 수 있는 경우의 수를 한 줄에 공백없이 출력한다.

### 예시 1
#### 입력
{% highlight css %}
5 2
930503 930503 890412 670610 680525
{% endhighlight %}
#### 출력
{% highlight css %}
3
{% endhighlight %}

# 풀이

### 설명
문제 2J처럼 sliding window 방법을 이용했습니다. 처음에 생년월일을 입력받고, 생년월일은 최대 6자리이므로 빈도수를 나타내는 배열 frequency를 1000000자리 할당했습니다. 그리고 처음 k개의 생년월일을 frequency 배열에 처리해주었습니다. 현재 모두 0으로 초기화 되어 있으므로 생년월일을 인덱스로 하는 value를 +1 해 주었습니다. 해당 연산은 add_birthdate함수에서 수행하였고 이 함수는 언급한 행동을 처리함과 동시에 빈도수가 1이 되면 글로벌 변수인 unique를 +1 해주고, 아니라면 -1을 하는 명령을 수행합니다. del_birthdate함수도 이와 비슷한 원리로 작동합니다. 다만 한 번의 연산이 끝나고 나서 unique변수를 그대로 사용하는 것이 아니라 unique변수가 k와 같을 때, 즉 모두 생년월일이 다를 때 cnt변수를 +1 카운팅해주고 이 cnt변수를 이용합니다. 시간복잡도는 O(min(n, n-k))인데 k의 최소 수는 상수이고 이를 무시한다고 가정하면 최악의 경우 O(N)이 됩니다.

### 코드
{% highlight css %}
unique = 0
def add_birthdate(frequency, idx) :
	global unique
	frequency[idx] += 1
	if(frequency[idx] == 1) : unique += 1
	else : unique -= 1

def del_birthdate(frequency, idx) :
	global unique
	frequency[idx] -= 1
	if(frequency[idx] == 1) : unique += 1
	else : unique -= 1
		
n, k = map(int, input().split())
birthdate = list(map(int, input().split()))
frequency = [0] * 1000000
cnt = 0
for i in range(k) :
	add_birthdate(frequency, birthdate[i])
if(unique == k) : cnt += 1
for i in range(n-k) :
	del_birthdate(frequency, birthdate[i])
	add_birthdate(frequency, birthdate[i+k])
	if(unique == k) : cnt += 1
print(cnt)
{% endhighlight %}

### 기타
- `Memory` : 28258
- `Time` : 0.19