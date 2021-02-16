---
layout: post
title: "알고리즘 문제해결기법 입문 문제3I"
date: 2021-02-16
excerpt: "C++, Python 알고리즘 문제해결기법 입문 문제3I"
tags: [C++, Python, 알고리즘 문제해결기법 입문, Chapter.3]
comments: true
---
# 3I

### 문제
지수가 살고 있는 이상한 나라에서는 독특한 복권제도가 존재한다. 이상한 나라에서는 매 주 당첨 될 자연수 번호를 정해두며, 복권을 구매한 사람은 그 자리에서 수 많은 카드들 중 하나를 뽑을 수 있는 기회가 세 번 주어진다. 즉, 똑같은 카드를 세 번 뽑을 수 도 있다. 이렇게 세 번에 걸쳐 뽑은 카드들에 적혀있는 세 자연수를 더하여 당첨 번호로 지정된 자연수와 일치한다면 그 사람은 당첨되는 것이다.

복권 담당자인 미주는 이번 주에 복권에 사용 될 당첨 번호들을 정하려고 한다. 하지만 매 번 실제로 그 당첨번호가 세 카드에 적힌 숫자들의 합으로 만들어 질 수 있는지 (즉, 실제로 당첨될 수 있는 번호인지) 검사하는 과정이 너무 번거로워 고민을 하고 있다. 미주를 도와서 주어진 카드를 조합해 당첨 번호들을 만들 수 있는지 판단하는 프로그램을 작성해주자.

### 입력 형식
첫 줄에는 사용할 카드의 수 N과 당첨 번호의 숫자 M이 공백으로 구분되어 주어진다. N은 1이상 1,000이하의 자연수이며 M은 1이상 100이하의 자연수이다.

두 번째 줄에는 N개의 카드에 적힌 숫자들이 공백으로 구분되어 1이상 1억 이하의 자연수로 주어진다. 

세 번째 줄에는 M개의 이번 주에 사용 될 당첨번호들이 공백으로 구분되어 주어진다. 당첨번호들은 모두 서로다른 1이상 3억 이하의 자연수이다. 

### 출력 형식
M개의 당첨번호 들 중 실제로 세 카드에 적힌 숫자의 합으로 표현될 수 있는 당첨번호들을 모두 출력한다.

- 실제로 만들 수 있는 당첨번호가 여러개라면, 오름차순으로 정렬하고 각 숫자는 공백으로 구분하여 한 줄에 출력한다.
- 실제로 만들 수 있는 당첨번호가 존재하지 않는다면 NO를 출력한다.

### 예시 1
#### 입력
{% highlight css %}
3 5
1 2 3
1 2 3 4 5
{% endhighlight %}
#### 출력
{% highlight css %}
3 4 5
{% endhighlight %}

### 예시 2
#### 입력
{% highlight css %}
10 5
1 2 3 4 5 6 7 8 9 10
1 2 20 30 40
{% endhighlight %}
#### 출력
{% highlight css %}
20 30
{% endhighlight %}

# 풀이

### 설명
3H와 같은 풀이법이지만 반복문을 세 개를 쓴다는 점에서 차이가 있습니다. 또, vector를 이용하여 가능한 target들을 저장해놓고 함수 내부에서 vector를 정렬하여 반환하는 방식을 이용합니다. 처음에는 내부반복문들의 종점이 n까지로 설정했지만 그러면 똑같은 계산을 여러번 하게 되는 일이 발생합니다. 그렇기 때문에 마지막 반복문을 이전 내부 반복문의 변수를 종점으로 두어서 중복으로 계산하는 일이 없게 만들었습니다. 

### 코드
#### C++
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
vector<int> getPossibleTargets(int n, int m, int * cards, int* targets) {
	sort(cards, cards+n);
	vector<int> possibleTargets; // 만들 수 있는 당첨 번호들
	for (int i = 0;i<m;i++)
	{
		int t = targets[i];
		bool possible = false;
		for(int j = 0;j<n;j++)
		{
			int x = cards[j];
			for(int k = 0;k<=j;k++)
			{
				int y = cards[k];
				int z = t - (x + y);
				if(binary_search(cards, cards+n, z) == true)
				{
					possible = true;
					break;
				}
			}
		}
		if(possible == true)
		{
			possibleTargets.push_back(t);
		}
	}
	sort(possibleTargets.begin(), possibleTargets.end());

	return possibleTargets;
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

	vector<int> answers = getPossibleTargets(n, m, cards, targets);

	if (answers.size() == 0)
	{ 	// 가능한 당첨번호가 없다면 NO를 출력한다
		printf("NO");
	}
	else
	{ //가능한 당첨번호가 존재한다면 그 목록을 출력한다.
		for (int i = 0; i < answers.size(); i++)
		{
			if (i > 0)
			{
				printf(" ");
			}
			printf("%d", answers[i]);
		}
	}

	delete[] cards;
	delete[] targets;

	return 0;
}
{% endhighlight %}

### 기타
#### C++
- `Memory` : 3108
- `Time` : 0.046