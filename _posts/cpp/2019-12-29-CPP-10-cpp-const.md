---
layout: single
title:  "10.C++ 한정자(const)"
permalink: /categories/:categories/:title:output_ext
taxonomy: {title}
categories: C++
tags: C++ const
comments: true
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
<br>

## 1. 한정자의 이해

한정자는 보통 1회성 변수로 한번 설정 한 이후 변경되지 않는 변수에 많이 활용하게 된다. 주로 API key 혹은 임베디드 시스템 환경에서 PIN 번호로 활용하기도 한다. 물론 #define을 활용한 매크로도 많이 활용되긴 하지만 말이다.

한정자는 변수(또는 객체) 앞에 선언하여 값을 변경 할 수 없도록 지정하는 문법이다. 

```
const 변수(또는 객체)
```


{% highlight c++ linenos %}
using namespace std;

int getSize(){
	return 200;
}

int main(){
	const int size = 100;
	const int bufferSize = getSize();
	size = 200;// 컴파일 오류 (변경 불가능)
	const int count; // 컴파일 오류 (초기값 필요)
	return 0;
}

{% endhighlight %}

size 변수는 const 변수이기 때문에 재정의가 불가하다. 또한, bufferSize 런타임 과정에서 return 값을 반환 받아 정의하게 된다.

## 2. 외부 참조 한정자 extern 키워드

만약 현재 CPP 파일 말고 다른 CPP 파일에서 활용하고 싶다면, `extern` 키워드를 활용하여 사용할 수 있다.

* extern.h 파일
{% highlight c++ linenos %}
extern const int bufferSize = 200;
extern const char[20] domain = "www.memaker.co.kr";
{% endhighlight %}

* extern const 접근 파일1.cpp 
{% highlight c++ linenos %}
#include <iostream>
#include "extern.h"
using namespace std;
int main(){
	cout << bufferSize << ", " << domain <<endl;
	return 0;
}
{% endhighlight %}

* extern const 접근 파일2.cpp
{% highlight c++ linenos %}
#include <iostream>
#include "extern.h"
using namespace std;
int main(){
	cout << bufferSize << ", " << endl;
	return 0;
}
{% endhighlight %}

## 3. 참조자를 한정자로 지정

다음과 같이 참조자 역시 한정자로 지정할 수 있다.

{% highlight c++ linenos %}
int main(){
	const int size = 100;

	const int &size2 = size;
	int &size3 = size; // 컴파일 오류 발생
	return 0;
}
{% endhighlight %}

한정자를 초기값으로 참조자를 선언할 때는 반드시 해당 참조자 역시 const 키워드를 붙여서 한정자로 선언해야 한다.

[출처:최신 표준 C++로 쉽고 빠르게 안내하는 모던 C++ 프로그래밍]
