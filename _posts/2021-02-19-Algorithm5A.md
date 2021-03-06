---
layout: post
title: "알고리즘 문제해결기법 입문 문제5A"
date: 2021-02-19
excerpt: "Python 알고리즘 문제해결기법 입문 문제5A"
tags: [Python, 알고리즘 문제해결기법 입문, Chapter.5]
comments: true
---
# 5A

### 문제
어느 한 도시에서는 공장 단지가 부도가 나게 되어 넓은 공터가 경매에 올라오게 되었다. 이 공터는 가로와 세로가 각각 N km인 정사각형 모양이며 가로와 세로가 1 km인 정사각형 격자 모양으로 영역을 나누어 개별적으로 판매하고 있다. 

그 도시에 살고있던 한 부자 경영인은 평소 자신이 기획해오던 놀이공원 건설 프로젝트를 몰래몰래 진행하기로 결정하였다. 때마침 경매에 올라온 이 공터에 관심을 가지게 된 경영인은 판매 중인 땅들 중 일부에는 기존의 공장에서 배출 된 폐기물들이 방치되어 있다는 사실을 알게 되었다. 놀이공원 건설을 위해서는 가로로 K km, 세로로 K km인 정사각형 모양의 영역이 필요한데, 당연히 놀이공원 건설을 위해서는 해당 영역의 폐기물들을 모두 처리해야만 한다.

NxN 격자 모양의 공터에서 KxK 정사각형 크기의 땅을 구매하려고 할 때, 구매할 땅에 포함 된 폐기물의 수를 최소로 할 수 있는 영역을 찾을 수 있는 프로그램을 작성해주자.

### 입력 형식
첫 줄에는 테스트케이스의 수를 나타내는 1이상 100이하의 자연수 T가 주어진다.

각 테스트케이스의 첫 줄에는 두 자연수 공터의 크기를 나타내는 N과 구매할 땅의 크기를 나타내는 K가 주어진다.

- N은 1이상 100이하의 자연수이다.
- K는 1이상 10이하의 자연수이다. K는 N보다 작거나 같은 값을 가진다.

이후 N줄에 걸쳐서 공터의 각 행의 정보가 차례로 주어진다.

- 각 줄은 공백으로 구분 된 0과 1이 총 N개 주어진다.
- 0은 비어있는 땅을 나타내며, 1은 폐기물이 존재하는 칸을 나타낸다

### 출력 형식
각 테스트케이스에 대하여 KxK 모양의 땅을 구매했을 때 얻을 수 있는 최소의 폐기물의 수를 공백없이 한 줄에 출력한다.

### 예시 1
#### 입력
{% highlight css %}
1
5 3
1 0 0 1 0
0 1 0 0 1
0 0 0 1 0
0 0 0 0 0
0 0 1 0 0
{% endhighlight %}
#### 출력
{% highlight css %}
1
{% endhighlight %}

### 예시 2
#### 입력
{% highlight css %}
3
5 3
1 0 0 1 0
0 1 0 0 1
0 0 0 1 0
0 0 0 0 0
0 0 1 0 0
5 3
0 0 0 0 0
0 0 0 0 0
0 0 0 0 0
0 0 0 0 0
0 0 0 0 0
5 3
1 1 1 1 1
1 1 1 1 1
1 1 1 1 1
1 1 1 1 1
1 1 1 1 1
{% endhighlight %}
#### 출력
{% highlight css %}
1
0
9
{% endhighlight %}

# 풀이

### 설명
주어지는 배열의 크기가 그렇게 크지 않으므로 모든 배열을 다 돌아보는 알고리즘을 적용했습니다. 다만, n-k이후에 나오는 인덱스는 k크기만큼 조사를 할 수 없으므로 n-k까지 for문을 설정했습니다. 조사할 인덱스가 결정이 되면 이를 find_trash라는 배열에 주어 폐기물이 존재하는지 검사를 했습니다. 폐기물은 배열에서 1에 해당하므로 trash라는 0으로 초기화 된 변수를 두어 1씩 업데이트를 했습니다. 문제에서는 최소의 폐기물을 구하라고 했으므로 min_trash변수와 find_trash함수에서 리턴되는 값의 최소를 비교해 min_trash에 업데이트를 해주는 방식을 거쳤고, min_trash의 최댓값은 모든 k칸의 정사각형이 폐기물로 차 있을 때가 되므로 k*k로 초기화했습니다.

### 코드
{% highlight css %}
import sys

def find_trash(arr, k, row, column) :
	trash = 0
	for i in range(row, row+k) :
		for j in range(column, column+k) :
			if(arr[i][j] == 1) : trash += 1
	return trash

t = int(input())
for _ in range(t) :
	n, k = map(int, sys.stdin.readline().split())
	arr = [list(map(int, sys.stdin.readline().split())) for _ in range(n)]
	min_trash = k*k
	for i in range(n-k+1) :
		for j in range(n-k+1) :
			min_trash = min(min_trash, find_trash(arr, k, i, j))
	print(min_trash)
{% endhighlight %}

### 기타
- `Memory` : 9676
- `Time` : 0.678