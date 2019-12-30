---
layout: single
title:  "09.C++ 참조자(reference)"
permalink: /categories/:categories/:title:output_ext
taxonomy: {title}
categories: C++
tags: C++ reference
comments: true
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
<br>

## 1. 참조자의 이해

참조자를 선언하려면 다음처럼 주소 연산자(&)를 변수명 앞에 지정한다.

{% highlight c++ linenos %}
using salary = double; //별칭 선언
salary kiho = 100.12;//salary형으로 kiho 변수 선언

salary kiho = 100.12;
salary &john = kiho;
{% endhighlight %}

이렇게 선언하면 john 변수는 salary형으로 선언한 kiho를 참조하게 되며 kiho 변수의 별칭이 된다.

{% highlight c++ linenos %}
#include <iostream>
using namespace std;
int main(){
	using salary = double;
	salary kiho = 100.12;
	salary &john = kiho;

	cout << "kiho's memory address = " << &kiho << endl;
	cout << "john's memory address = " << &john << endl;

	return 0;
}

{% endhighlight %}

터미널에서 본 결과값.

```
kiho's memory address = 0017F828
john's memory address = 0017F828
```

오류가 나는 경우.

{% highlight c++ linenos %}
using salary = double;
salary kiho = 100.12;
salary &john; //오류(별칭을 지정할 초기값 필요)
{% endhighlight %}

{% highlight c++ linenos %}
#include <iostream>
using namespcae std;

int main(){
	int val1 = 100;
	int &val2 = val1;
	int &val3 = 200; // 상수 대입 에러
	int &val4 = val2;
	int &val5;  // 변수 초기값 에러
	val1 = val1 * 3;

	cout << "val1 = " << val1 << endl;
	cout << "val2 = " << val2 << endl;
	cout << "val4 = " << val4 << endl;

	return 0;

}
{% endhighlight %}

```
val1 = 300;
val2 = 300;
val3 = 300;
```

[출처:최신 표준 C++로 쉽고 빠르게 안내하는 모던 C++ 프로그래밍]
