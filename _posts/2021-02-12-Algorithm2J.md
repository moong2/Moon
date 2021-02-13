---
layout: post
title: "알고리즘 문제해결기법 입문 문제2J"
date: 2021-02-12
excerpt: "Python 알고리즘 문제해결기법 입문 문제2J"
tags: [Python, 알고리즘 문제해결기법 입문, Chapter.2]
comments: true
---
# 2J

### 문제
같은 반인 현무와 재윤이는 이번 주 청소 당번이다. 현무와 재윤이는 서로 내기를 하여 청소일을 한 명에게 몰아주기로 하였다. 간단한 게임을 통해 지는 사람이 두 명분의 청소를 하기로하고 재윤이는 아래와 같은 게임을 현무에게 제안하였다.

- 재윤이는 총 N개의 종이컵의 안 쪽에 임의의 자연수를 적어둔다.
- 모든 종이컵은 숫자가 보이지 않도록 뒤집은 채로 일렬로 나열한다.
- 종이컵의 위치는 게임 도중에 변경될 수 없다.
- 현무는 임의의 인접한 K개의 연속된 종이컵을 선택하여 숫자를 확인하고 그 숫자들의 합을 구한다.
- 해당 숫자들의 합이 짝수이면 재윤이가 청소를 하고, 홀수이면 현무가 청소를 한다.
 
게임을 시작하기 전 현무는 재윤이가 숫자들을 자신이 이길 수 밖에 없도록 조작한 것이 아닌지 의심을 하게되었다. 하지만 재윤이가 워낙에 많은 종이컵을 준비해두었기에 일일이 확인을 해보기는 힘들었다. 현무는 당신에게 재윤이가 적은 숫자들로 게임을 진행할 경우 자신이 이길 수 있는 경우가 존재하는지 확인해달라는 부탁을 하였다. 현무를 위해 프로그램을 만들어주자.

### 입력 형식
첫 줄에는 종이컵의 수 N과 현무가 선택할 종이컵의 수 K가 공백으로 구분되어 주어진다. N과 K는 1이상 10만 이하의 자연수이다.

두 번째 줄에는 총 N개의 종이컵에 적힌 숫자들이 실제 놓여진 순서대로 주어진다. 종이컵에 적힌 숫자들은 모두 0이상 100만 이하의 정수이다.

### 출력 형식
첫 줄에 현무가 이겨서 재윤이가 청소를 하게 될 수 있는 경우의 수가 존재한다면 YES를 출력하고, 그렇지 않다면 NO를 출력한다.

### 예시 1
#### 입력
{% highlight css %}
3 2
1 2 3
{% endhighlight %}
#### 출력
{% highlight css %}
NO
{% endhighlight %}

### 예시 2
#### 입력
{% highlight css %}
4 2
1 2 3 3
{% endhighlight %}
#### 출력
{% highlight css %}
YES
{% endhighlight %}

### 예시 3
#### 입력
{% highlight css %}
5 1
2 2 2 2 2
{% endhighlight %}
#### 출력
{% highlight css %}
YES
{% endhighlight %}

# 풀이

### 설명
처음 반복문을 이용해서 이중 반복문을 돌 때는 시간초과가 떴습니다. 처음 sum_k에 0 인덱스부터 k개의 값을 더해준 것을 반복문을 돌며 업데이트 해주는 방식으로 해서 해결했습니다. 종점은 n-k+1로 설정을 했고, sum_k에 i-1원소의 값을 제거해주고 i+k-1 인덱스의 원소의 값을 추가했습니다. 시간복잡도는 O(N)입니다.

### 코드
{% highlight css %}
n, k = map(int, input().split())
num_li = list(map(int, input().split()))

is_win = False
sum_k = 0

for i in range(0, k) :
	sum_k += num_li[i]
if(sum_k % 2 == 0) : is_win = True
	
for i in range(1, n-k+1) :
	sum_k -= num_li[i-1]
	sum_k += num_li[i+k-1]
	if(sum_k % 2 == 0) : 
		is_win = True
		break
if(is_win == True) : print('YES')
else : print('NO')
{% endhighlight %}

### 기타
- `Memory` : 18584
- `Time` : 0.057