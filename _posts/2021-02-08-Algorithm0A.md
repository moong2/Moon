---
layout: post
title: "알고리즘 문제해결기법 입문 문제0A"
date: 2021-02-08
excerpt: "Python 알고리즘 문제해결기법 입문 문제0A"
tags: [Python, 알고리즘 문제해결기법 입문, Chapter.0]
comments: true
---
# 0A

### 문제
표준 출력함수를 통해 Hello World!을 출력하는 프로그램을 작성하시오.

### 입력 형식
이 문제는 별도의 입력이 주어지지 않는다.

### 출력 형식
한 줄에 Hello World!를 출력한다.
- ❕ 단, 대소문자나 공백의 위치가 다른 문자는 오답으로 인정한다.

### 예시1
{% highlight css %}
Hello World!
{% endhighlight %}

# 풀이
{% highlight css %}
board = []
for _ in range(10) :
    board.append(list(map(int, input().split())))
x, y = 1, 1
if(board[x][y] != 2) :
    board[x][y] = 9
    while(True) :
        if(board[x+1][y] == 1 and board[x][y+1] == 1) : break
        if(board[x][y+1] == 0) : 
            board[x][y+1] = 9 
            y += 1
        elif(board[x][y+1] == 1) : 
            if(board[x+1][y] == 2) :
                board[x+1][y] = 9
                break
            board[x+1][y] = 9
            x += 1
        else : 
            board[x][y+1] = 9
            break
else :
    board[x][y] = 9
for i in range(10) :
    for j in range(10) :
        print(board[i][j], end=' ')
    print('')
{% endhighlight %}