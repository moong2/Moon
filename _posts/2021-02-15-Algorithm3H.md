---
layout: post
title: "알고리즘 문제해결기법 입문 문제3H"
date: 2021-02-15
excerpt: "C++, Python 알고리즘 문제해결기법 입문 문제3H"
tags: [C++, Python, 알고리즘 문제해결기법 입문, Chapter.3]
comments: true
---
# 3F

### 문제
지애가 살고 있는 이상한 나라에서는 독특한 복권제도가 존재한다. 이상한 나라에서는 매 주 당첨 될 자연수 번호를 정해두며, 복권을 구매한 사람은 그 자리에서 수 많은 카드들 중 하나를 뽑을 수 있는 기회가 두 번 주어진다. 즉, 똑같은 카드를 두 번 뽑을 수 도 있다. 이렇게 두 번에 걸쳐 뽑은 카드들에 적혀있는 두 자연수를 더하여 당첨 번호로 지정된 자연수와 일치한다면 그 사람은 당첨되는 것이다.

복권 담당자인 미주는 이번 주에 복권에 사용 될 당첨 번호들을 정하려고 한다. 하지만 매 번 실제로 그 당첨번호가 두 카드에 적힌 숫자들의 합으로 만들어 질 수 있는지 (즉, 실제로 당첨될 수 있는 번호인지) 검사하는 과정이 너무 번거로워 고민을 하고 있다. 미주를 도와서 주어진 카드를 조합해 당첨 번호들을 만들 수 있는지 판단하는 프로그램을 작성해주자.

### 입력 형식
첫 줄에는 사용할 카드의 수 N과 당첨 번호의 수 M이 공백으로 구분되어 주어진다. N은 1이상 10만이하의 자연수이며 M은 1이상 100이하의 자연수이다.

두 번째 줄에는 N개의 카드에 적힌 숫자들이 공백으로 구분되어 1이상 1억 이하의 자연수로 주어진다. 

세 번째 줄에는 M개의 이번 주에 사용 될 당첨번호들이 공백으로 구분되어 주어진다. 당첨번호들은 모두 서로다른 1이상 2억 이하의 자연수이다. 

### 출력 형식
M개의 당첨번호 들 중 실제로 두 카드에 적힌 숫자의 합으로 표현될 수 있는 당첨번호의 개수를 정수로 출력한다.

### 예시 1
#### 입력
{% highlight css %}
5 3
1 9 2 7 3
6 7 8
{% endhighlight %}
#### 출력
{% highlight css %}
2
{% endhighlight %}

# 풀이

### 설명
정렬을 하여 이진탐색을 하는 방법을 사용했습니다. 파이썬에서는 시간초과가 나서 C++로 일단 풀이를 작성했습니다.

### 코드
#### C++
{% highlight css %}
#include <stdio.h>
#include <vector>
#include <algorithm>

using namespace std;

/**
* 중복을 포함해 두 카드의 합으로 만들 수 있는 당첨번호의 수를 계산하는 함수
* @param n     카드의 수
* @param m     검사하려는 당첨번호의 수
* @param cards   각 카드에 적힌 숫자들
* @param target  검사하려는 각 당첨번호 리스트
* @return
*/
int getPossibleTargetNumber(int n, int m, int * cards, int* targets) {
	sort(cards, cards + n);
	int answer = 0;
	for(int i = 0;i < m;i++)
	{
		int k = targets[i];
		bool possible = false;
		for(int j = 0;j<n; j++)
		{
			int x = cards[j];
			int y = k - x;
			if(binary_search(cards, cards+n, y) == true)
			{
				possible = true;
				break;
			}
		}
		if(possible == true){answer++;}
	}
	return answer;
}

int main() {
	int n;	// 카드의 수 
	int m;	// 검사 할 후보 당첨번호의 수 
	scanf("%d %d", &n, &m);

	int* cards = new int[n];
	int* targets = new int[m];

	// 각 카드 정보를 입력받는다
	for (int i = 0; i < n; i++){
		scanf("%d", &cards[i]);
	}

	// 각 후보 당첨번호를 입력받는다
	for (int i = 0; i < m; i++){
		scanf("%d", &targets[i]);
	}

	int answer = getPossibleTargetNumber(n, m, cards, targets);

	printf("%d\n", answer);


	delete[] cards;
	delete[] targets;

	return 0;
}

{% endhighlight %}

### 기타
#### C++
- `Memory` : 3160
- `Time` : 0.006