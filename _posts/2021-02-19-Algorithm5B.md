---
layout: post
title: "알고리즘 문제해결기법 입문 문제5B"
date: 2021-02-19
excerpt: "Python 알고리즘 문제해결기법 입문 문제5B"
tags: [Python, 알고리즘 문제해결기법 입문, Chapter.5]
comments: true
---
# 5B
**이 문제의 코드는 80점을 받은 코드입니다.**

### 문제
어느 한 도시에서는 공장 단지가 부도가 나게 되어 넓은 공터가 경매에 올라오게 되었다. 이 공터는 가로와 세로가 각각 N km인 정사각형 모양이며 가로와 세로가 1 km인 정사각형 격자 모양으로 영역을 나누어 개별적으로 판매하고 있다. 

그 도시에 살고있던 한 부자 경영인은 평소 자신이 기획해오던 놀이공원 건설 프로젝트를 몰래몰래 진행하기로 결정하였다. 때마침 경매에 올라온 이 공터에 관심을 가지게 된 경영인은 판매 중인 땅들 중 일부에는 기존의 공장에서 배출 된 폐기물들이 방치되어 있다는 사실을 알게 되었다. 놀이공원 건설을 위해서는 가로로 K km, 세로로 K km인 정사각형 모양의 영역이 필요한데, 당연히 놀이공원 건설을 위해서는 해당 영역의 폐기물들을 모두 처리해야만 한다.

NxN 격자 모양의 공터에서 KxK 정사각형 크기의 땅을 구매하려고 할 때, 구매할 땅에 포함 된 폐기물의 수를 최소로 할 수 있는 영역을 찾을 수 있는 프로그램을 작성해주자.

### 입력 형식
첫 줄에는 테스트케이스의 수를 나타내는 1이상 100이하의 자연수 T가 주어진다.

각 테스트케이스의 첫 줄에는 두 자연수 공터의 크기를 나타내는 N과 구매할 땅의 크기를 나타내는 K가 주어진다.

- N은 1이상 300이하의 자연수이다.
- K는 1이상 300이하의 자연수이다. K는 N보다 작거나 같은 값을 가진다.

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

# 풀이

### 설명
슬라이딩 윈도우 알고리즘을 이용했습니다. offset은 조사할 column이 0일 때이므로 이 때는 find_trash함수를 이용합니다. 그리고 1부터 n-k+1까지 column을 옮겨갑니다. 이 때, 계산하지 않을 column을 old_column 계산해야 할 새로운 column을 new_column이라고 했습니다. old_column은 현재 column인덱스의 -1번째에 해당하고, new_column은 현재 인덱스와 k만큼 떨어진 인덱스에 해당합니다. 이 때, 열을 현재 열부터 k만큼 떨어진 열까지 조사를 하며 old_column에 폐기물이 있을 시 trash_slide에서 폐기물의 수를 빼주고, new_column에 폐기물이 있을 시 trash_slide에서 폐기물의 수를 더해줍니다. 그리고 답이 될 trash와 비교를 하여 최소인 값을 trash에 저장합니다. 

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
	trash = k**2
	for i in range(n-k+1) :
		trash_slide = find_trash(arr, k, i, 0)
		trash = min(trash, trash_slide)
		for j in range(1, n-k+1) :
			old_column, new_column = j-1, j+k-1
			for l in range(i, i+k) :
				if(arr[l][old_column] == 1) : trash_slide -= 1
				if(arr[l][new_column] == 1) : trash_slide += 1
			trash = min(trash, trash_slide)
	print(trash)
{% endhighlight %}

### 기타
- `Memory` : 9750
- `Time` : 0.4725