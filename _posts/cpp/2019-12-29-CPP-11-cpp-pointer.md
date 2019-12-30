---
layout: single
title:  "11.C++ 포인터(pointer)"
permalink: /categories/:categories/:title:output_ext
taxonomy: {title}
categories: C++
tags: C++ pointer
comments: true
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
<br>

## 1. 포인터

C/C++을 통틀어 가장 중요한 개념으로 여겨지는 포인터는 해당 언어를 포기하게 하는 주범이다. 사실 차근차근 따라가면 이해가 되는데, 꼬아 놓으면 진짜 답없는 게 또 이 포인터가 아닌가 싶다.
어쨌든 이 모던 C++에서 다루는 내용은 기본적인 C의 포인터 개념이라기 보단, C++ 11 이상에서 어떻게 활용되는지 그리고 앞으로 스마트 포인터라는 개념도 배우게 될텐데 기본부터 잘 읽혀가는 것이 중요할 것 같다.

> 포인터 : 참조자와 유사하게 주소로 특정 변수나 객체를 잠조할 수 있다. 다시말해, 포인터 변수에는 다른 변수의 주소값을 저장하여, 해당 주소의 데이터를 트랙킹할 수 있다.


{% highlight c++ linenos %}
int value = 100;
int *ptrValue = &value;
{% endhighlight %}

현재 두 변수 사이에 관계는 아래 표와 같이 나타낼 수 있다.

|변수명|value|ptrValue|
|---
|값|100|65344|
|메모리주소|65344|65342|

{% highlight c++ linenos %}
#include <iostream>

using namespace std;
int main(){
	int value = 100;
	int *ptrValue = &value;

	cout << value << endl;
	cout << &value << endl;
	cout << ptrValue << endl;
	cout << *ptrValue << endl;
	cout << &ptrValue << endl;

	int **pptrValue = &ptrValue;
	
}

{% endhighlight %}

위 내용을 완전히 이해 한다면, 대충 포인터의 개념은 잡혔다고 생각해도 좋을 것 같다.

## 2. null 포인터

포인터 변수는 될수 있으면 선언할 때 null 포인터로 초기화 해주는 것이 좋다. 이는 초기화가 안된 포인터 변수의 Garbage로 인해 런타임 메모리 오류를 일으킬 수 있는 소지를 미연에 방지할 수 있다.

```
int *p = nullptr;
```

## 3. void 포인터

C++ 11 표준 부터 재미있는 포인터의 개념들이 나오기 시작했다. void 포인터는 참조자변수의 타입을 지정하지 않아도 auto와 같이 자동으로 할당해주는 기능을 갖추고 있다. 기존의 C언어는 노가다 성이 짙었는데, 모던 C++은 더 편리해진 느낌이다.

{% highlight c++ linenos %}
int value = 100;
doble value2 = 100.121;

void *voidPtr = &value;
voidPtr = &value2;
{% endhighlight %}



[출처:최신 표준 C++로 쉽고 빠르게 안내하는 모던 C++ 프로그래밍]
