---
layout: post
title: "알고리즘 문제해결기법 입문 문제4G"
date: 2021-02-18
excerpt: "Python 알고리즘 문제해결기법 입문 문제4G"
tags: [Python, 알고리즘 문제해결기법 입문, Chapter.4]
comments: true
---
# 4G

### 문제
프로그래머 지수는 제비뽑기 프로그램을 만들고 있다. 자신이 이미 정해둔 N개의 배열에 각각 임의의 번호들을 저장해 두고 사용자들이 0~(N-1)의 정수 번호를 하나 입력하면 그 칸에 있는 숫자를 알려주게 된다. 하지만 자신의 제비뽑기 프로그램을 사람들이 사용하는 모습을 지켜보던 지수는 배열에 저장된 데이터들이 고정적이기 때문에 게임을 반복할 수록 사람들이 숫자를 추정할 수 있다는 문제점을 발견했다. 

그래서 지수는 아래와 같은 두 가지 기능을 구현하여 주기적으로 배열에 저장된 원소들의 위치들을 바꿔주고자 한다.

- 배열의 원소들을 모두 왼쪽으로 한 칸씩 옮긴다. 이 때 0번 칸에 있던 원소는 (N-1)번 칸으로 이동된다.
- 배열의 원소들을 모두 오른쪽으로 한 칸씩 옮긴다. 이 때 (N-1)번 칸에 있던 원소는 0번 칸으로 이동된다.


하지만 위의 두 동작은 너무 단순하기 때문에 실제로는 위의 기능을 응용하여 아래와 같은 네 가지 명령어를 구현하고자 한다.

- 입력으로 0 P 가 주어지면 화면에 현재 배열의 P번 칸에 있는 원소를 한 줄에 출력해준다.
- 입력으로 1 K 가 주어지면 현재 배열을 왼쪽으로 한 칸씩 옮기는 동작을 총 K번 수행한다.
- 입력으로 2 K 가 주어지면 현재 배열을 오른쪽으로 한 칸씩 옮기는 동작을 총 K번 수행한다.
- 입력으로 3 이 주어지면 배열을 한 칸도 좌우로 이동하지 않았던 초기 상태로 되돌린다.


아직 프로그래밍이 서툰 지수를 도와 위의 네 명령어를 처리하는 프로그램을 작성해주자.

### 입력 형식
첫 줄에는 배열의 크기 N과 처리할 명령어의 수 M이 공백으로 구분 된 두 자연수로 주어진다. N과 M은 모두 1,000이하의 자연수이다.

두 번째 줄에는 초기 배열에 존재하는 N개의 자연수들이 공백으로 구분되어 순서대로 주어진다. 배열의 모든 원소는 1,000이하의 자연수이다.

이후 총 M줄에 걸쳐서 한 줄에 하나씩 네 가지 명령어 중 하나가 주어진다.

- 각 명령어의 처리 방법은 문제 설명과 예시를 참고한다.
- 0 P 명령어에서 P는 0이상 (N-1)이하의 정수이다.
- 1 K, 2 K 명령어에서 K는 1만 이하의 자연수이다.

### 출력 형식
입력으로 명령어 0 P 가 주어질 때 마다 배열의 P번 칸에 존재하는 원소를 한 줄에 출력한다.

### 예시 1
#### 입력
{% highlight css %}
5 7
1 2 3 4 5
0 3
1 5
0 2
2 3
0 0
3
0 0
{% endhighlight %}
#### 출력
{% highlight css %}
4
3
3
1
{% endhighlight %}

# 풀이

### 설명
배열을 다 옮기는 방법이 있지만 가장 왼쪽에 있는 원소가 원래 배열의 몇 번 인덱스인지를 구해 저장하면 상대적으로 그 위치를 알 수 있습니다. 왼쪽, 오른쪽으로 옮기는 것을 shift_left, shift_right 함수에서 수행했고 쉽게 관리를 해주기 위해서 클래스로 구현을 했습니다. 

### 코드
{% highlight css %}
import sys

class ShiftingArray :
	def __init__(self, len, array) :
		self.len = len
		self.array = array
		self.leftIndex = 0
		
	def get_p(self, p) :
		return (p + self.leftIndex) % self.len
		
	def shift_left(self, k) :
		k = k % self.len
		self.leftIndex = (self.leftIndex + k) % self.len
		
	def shift_right(self, k) :
		k = k % self.len
		self.leftIndex = (self.leftIndex - k + self.len) % self.len
		
	def shift_original(self) :
		self.leftIndex = 0
	
n, m = map(int, sys.stdin.readline().split())
array = list(map(int, sys.stdin.readline().split()))
shifting_array = ShiftingArray(n, array)

for _ in range(m) :
	command = sys.stdin.readline().split()
	if(command[0] == '0') :
		print(array[shifting_array.get_p(int(command[1]))])
	elif(command[0] == '1') :
		shifting_array.shift_left(int(command[1]))
	elif(command[0] == '2') :
		shifting_array.shift_right(int(command[1]))
	else :
		shifting_array.shift_original()
{% endhighlight %}

### 기타
- `Memory` : 9250
- `Time` : 0.02