---
layout: post
title: "알고리즘 문제해결기법 입문 문제3J"
date: 2021-02-16
excerpt: "C++, Python 알고리즘 문제해결기법 입문 문제3J"
tags: [C++, Python, 알고리즘 문제해결기법 입문, Chapter.3]
comments: true
---
# 3I

### 문제
예인이가 살고 있는 이상한 나라에서는 독특한 복권제도가 존재한다. 이상한 나라에서는 매 주 당첨 될 자연수 번호를 정해두며, 복권을 구매한 사람은 그 자리에서 수 많은 카드들 중 하나를 뽑을 수 있는 기회가 네 번 주어진다. 즉, 똑같은 카드를 네 번 뽑을 수 도 있다. 이렇게 네 번에 걸쳐 뽑은 카드들에 적혀있는 네 자연수를 더하여 당첨 번호로 지정된 자연수와 일치한다면 그 사람은 당첨되는 것이다.

복권 담당자인 미주는 이번 주에 복권에 사용 될 당첨 번호들을 정하려고 한다. 하지만 매 번 실제로 그 당첨번호가 네 카드에 적힌 숫자들의 합으로 만들어 질 수 있는지 (즉, 실제로 당첨될 수 있는 번호인지) 검사하는 과정이 너무 번거로워 고민을 하고 있다. 미주를 도와서 주어진 카드를 조합해 당첨 번호들을 만들 수 있는지 판단하는 프로그램을 작성해주자.

### 입력 형식
첫 줄에는 사용할 카드의 수 N과 당첨 번호의 숫자 M이 공백으로 구분되어 주어진다. N은 1이상 1,000이하의 자연수이며 M은 1이상 100이하의 자연수이다.

두 번째 줄에는 N개의 카드에 적힌 숫자들이 공백으로 구분되어 1이상 1억 이하의 자연수로 주어진다. 

세 번째 줄에는 M개의 이번 주에 사용 될 당첨번호들이 공백으로 구분되어 주어진다. 당첨번호들은 모두 서로다른 1이상 4억 이하의 자연수이다. 

두 번째 줄에는 N개의 카드에 적힌 숫자들이 공백으로 구분되어 1이상 1억 이하의 자연수로 주어진다. 

세 번째 줄에는 M개의 이번 주에 사용 될 당첨번호들이 공백으로 구분되어 주어진다. 당첨번호들은 모두 서로다른 1이상 3억 이하의 자연수이다. 

### 출력 형식
M개의 당첨번호 들 중 실제로 네 카드에 적힌 숫자의 합으로 표현될 수 있는 당첨번호들을 모두 출력한다.

- 실제로 만들 수 있는 당첨번호가 여러개라면, 오름차순으로 정렬하고 각 숫자는 공백으로 구분하여 한 줄에 출력한다.
- 실제로 만들 수 있는 당첨번호가 존재하지 않는다면 NO를 출력한다.

### 예시 1
#### 입력
{% highlight css %}
10 5
2 4 6 8 10 12 14 16 18 20
6 7 8 9 10
{% endhighlight %}
#### 출력
{% highlight css %}
8 10
{% endhighlight %}

### 예시 2
#### 입력
{% highlight css %}
5 3
1 2 3 4 5
1 2 3
{% endhighlight %}
#### 출력
{% highlight css %}
NO
{% endhighlight %}

# 풀이

### 설명
카드를 네 개를 선택하므로 둘 둘의 합으로 나누어 클래스에 저장하여 이진탐색으로 찾아나가는 방식을 이용했습니다. 먼저 클래스에 카드의 합을 저장합니다. 메모리를 아끼기 위해서 중복이 되는 부분이 없도록 클래스에 저장을 합니다. 해당 합을 저장한 클래스는 pairs라는 vector에 저장을 합니다. G, H, I와 다른 점은 내부반복문에서 cards의 변수를 직접 사용하는 것이 아니라 pairs라는 vector를 이용하는 것입니다. pairs에 저장된 CardPair 클래스를 꺼내서 그 합을 이용해 y를 구하고 y를 저장한 CardPair클래스 변수를 생성해 이진탐색을 합니다. 주석으로 처리되어 있는 부분 중 네 가지 카드가 어떤 카드인지 알 수 있다고 했는데 이를 구하기 위해서는 처음 초기화를 할 때 card를 함께 저장해야합니다. lower_bound(a, b, x)는 [a, b)범위에서 x이상인 첫 번째 원소의 위치를 반환합니다. 그 반대로 upper_bound가 있습니다. 

### 코드
#### C++
{% highlight css %}
#include<vector>
#include<algorithm>
#include<iostream>
#include<stdio.h>
using namespace std;

class CardPair{
public:
	// 두 개의 카드 조합을 나타내는 클래스
	int card1;
	int card2;
	int sumOfCards; //두 카드의 합

	//두 카드의 정보를 알 때
	CardPair(int sumOfCards = 0)
	{
		this->card1 = -1;
		this->card2 = -1;
		this->sumOfCards = sumOfCards;
	}

	// 두 카드의 정보를 모르고 합만 알 때
	CardPair(int card1, int card2)
	{
		this->card1 = card1;
		this->card2 = card2;
		this->sumOfCards = card1 + card1;
	}

	// 두 카드의 합으로 짝들의 대소 관계를 정의한다.
	bool operator < (const CardPair &o) const{
		return this->sumOfCards < o.sumOfCards;
	}
	bool operator == (const CardPair & o) const{
		return this->sumOfCards == o.sumOfCards;
	}
};

/**
* 중복을 포함해 네 카드의 합으로 만들 수 있는 당첨번호들의 리스트를 반환하는 함수
* @param n     카드의 수
* @param m     검사하려는 당첨번호의 수
* @param cards   각 카드에 적힌 숫자들
* @param target  검사하려는 각 당첨번호 리스트
* @return      네 카드의 합으로 표현될 수 있는 당첨번호들의 오름차순 리스트
*/
vector<int> getPossibleTargets(int n, int m, int* cards, int* targets)
{
	vector<int> possibleTargets; // 만들 수 있는 당첨 번호들
	vector<CardPair> pairs;
	for(int i = 0;i<n;i++)
	{
		for(int j = 0;j<=i;j++)
		{
			CardPair pair = CardPair(cards[i] + cards[j]);
			pairs.push_back(pair);
		}
	}
	sort(pairs.begin(), pairs.end());
	
	for(int i = 0;i<m;i++)
	{
		int t = targets[i];
		bool possible = false;
		for(int j = 0;j<pairs.size();j++)
		{
			CardPair knownPair = pairs[j];
			int x = knownPair.sumOfCards;
			int y = t - x;
			CardPair targetPair = CardPair(y);
			if(binary_search(pairs.begin(), pairs.end(), targetPair) == true)
			{
				possible = true;
				break;
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

int main()
{
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
	{ // 가능한 당첨번호가 없다면 NO를 출력한다
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
- `Memory` : 5121
- `Time` : 0.011