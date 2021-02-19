---
layout: post
title: "알고리즘 문제해결기법 입문 문제6A"
date: 2021-02-19
excerpt: "Python 알고리즘 문제해결기법 입문 문제6A"
tags: [Python, 알고리즘 문제해결기법 입문, Chapter.6]
comments: true
---
# 6A

### 문제
괄호 문자열(Parenthesis String, PS)은 두 개의 괄호 기호인 ‘(’ 와 ‘)’ 만으로 구성되어 있는 문자열이다. 그 중에서 괄호의 모양이 바르게 구성된 문자열을 올바른 괄호 문자열(Valid PS, VPS)이라고 부른다. 한 쌍의 괄호 기호로 된 “( )” 문자열은 기본 VPS 이라고 부른다. 만일 x 가 VPS 라면 이것을 하나의 괄호에 넣은 새로운 문자열 “(x)”도 VPS 가 된다. 그리고 두 VPS x 와 y를 접합(concatenation)시킨 새로운 문자열 xy도 VPS 가 된다. 예를 들어 “(())()”와 “((()))” 는 VPS 이지만 “(()(”, “(())()))” , 그리고 “(()” 는 모두 VPS 가 아닌 문자열이다. 

여러분은 입력으로 주어진 괄호 문자열이 VPS 인지 아닌지를 판단해서 그 결과를 YES 와 NO 로 나타내어야 한다. 

### 입력 형식
입력 데이터는 표준 입력을 사용한다. 입력은 T개의 테스트 데이터로 주어진다. 입력의 첫 번째 줄에는 입력 데이터의 수를 나타내는 정수 T가 주어진다. 각 테스트 데이터의 첫째 줄에는 괄호 문자열이 한 줄에 주어진다. 하나의 괄호 문자열의 길이는 2 이상 50 이하이다. 

### 출력 형식
출력은 표준 출력을 사용한다. 만일 입력 괄호 문자열이 올바른 괄호 문자열(VPS)이면 YES, 아니면 NO를 한 줄에 하나씩 차례대로 출력해야 한다. 

### 예시 1
#### 입력
{% highlight css %}
6
(())())
(((()())()
(()())((()))
((()()(()))(((())))()
()()()()(()()())()
(()((())()(
{% endhighlight %}
#### 출력
{% highlight css %}
NO
NO
YES
NO
YES
NO
{% endhighlight %}

# 풀이

### 설명
스택을 이용하여 '('가 등장할 시 스택에 PUSH하고 ')'가 나오면 스택에 있는 값을 POP하였습니다. 단순하게 이렇게 구현할 시 '('가 ')'보다 많을 때는 문제가 되지 않으나 역일 때 스택에 값이 없음에도 POP작업을 하는 코드를 수행할 수 있습니다. 그래서 POP을 할 때 스택에 값이 들어있는 지 여부를 확인하고 값이 없다면 vps를 False로 바꿔준 뒤 반복문을 빠져나왔습니다. 그 뒤 vps를 판단하는 방법은 두 가지가 있습니다. 이미 vps가 False일 때와 스택에 값이 남아있을 때 입니다. 이 두 조건은 vps가 False라는 것을 증명해주므로 NO를 출력하고 그 외에는 YES를 출력해 vps임을 증명합니다.

### 코드
{% highlight css %}
t = int(input())
for _ in range(t) :
	ps = input()
	ps_stack = list()
	vps = True
	for elem in ps :
		if(elem == '(') : ps_stack.append(elem)
		else : 
			if(len(ps_stack) > 0) : ps_stack.pop()
			else : 
				vps = False
				break
	if(vps == False or len(ps_stack) > 0) :
		print('NO')
	else : print('YES')
{% endhighlight %}

### 기타
- `Memory` : 9463	
- `Time` : 0.028