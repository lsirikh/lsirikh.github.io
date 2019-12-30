---
layout: single
title:  "12.C++ 형변환(conversion-typcast)"
permalink: /categories/:categories/:title:output_ext
taxonomy: {title}
categories: C++
tags: C++ conversion typecast
comments: true
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
<br>

## 1. 배열의 포인터 변환

배열을 포인터로 변환하여 주소 값 이동을 통해 쉽게 배열의 값을 접근 할 수 있다. 
다음 예제를 통해서 그 기능을 살펴 볼 수 있다.

{% highlight c++ linenos %}
#include <iostream>

using namespace std;

int main(){
	int i; 
	int arr[10];

	for (i = 0; i < 10; i++){
		arr[i] = i * 2;
	}

	int *ptr = arr;
	cout << arr[1] << endl;
	cout << *(ptr +1) << endl;
	return 0;
}


{% endhighlight %}


이 둘의 결과는 같다는 것을 알 수 있다.

```
2
2
```


## 2. 명시적 형변환

C에서는 타입 캐스트 (type cast)를 통해서 형변환을 하게 된다. C++ 및 모던 C++에서도 같은 기능을 확장 재공하는 것 같다.

```
cast-name<type>(expression)

* type 변환될 형
* expresssion 변환할 값
* cast-name static_cast, const_static, dynamic_cast, reinterpret_cast
```

### 2.1 static_cast 형변환

보통 산술연산 작업에서 정밀도가 변경되는 것을 방지하기 위한 강제 형변환하는 경우 활용되는 것 같다.

{% highlight c++ linenos %}
int main(){
	float i = 100.12345;
	double j = 200.12345;

	float count = static_cast<float>(j/i);
}

{% endhighlight %}

위 예제를 통해서 개발자의 실수로 정밀도가 변경되는 것을 방지하기 위해서 `static_cast`가 활용되었다는 것을 알 수 있다.

{% highlight c++ linenos %}
int main(){
	double d = 1212;
	void *p = &d;
	double *dp = static_cast<double *><p>;
}

{% endhighlight %}

위의 예는 `void 포인터`를 사용한 경우인데, 적절한지 사실 조금의문이 든다. 뭔가 좀 억지로 예를든 느낌이 들긴 하지만, double 형 변수 `d`의 주소를 가리키는 `void 포인터 `인 `p`는 일단 타입이 정해지지 않은 상태이다. 
그 상황에서 `*dp`에 대입하려고 한다면, `static_cast<double *><p>`라는 방법으로 명시적 캐스팅이 필요한 상황이 된다는 것을 보여주기 위해 만든 것 같으나 이렇게 하면 `void 포인터`의 사용이 무색해질 것 같다는 생각이 든다. 아직 초보인 내가 감히 평가하기는 어렵겠으나 아직까진 그런 느낌적인 느낌이다.


### 2.2 const_cast 형변환

한정자(const)로 지정한 변수의 한정자 속성을 없애는(?) 기능이라고 볼 수 있을 것 같다. 주의할 점은 한정자 속성만 변경하는 것이지 자료형을 `int`에서 `double`로 바꾸고 이런 것은 허용되지 않는다.

{% highlight c++ linenos %}
int main(){
	const char *cp;
	char *q = static_cast<char*>(cp);
	static_cast<string>(cp);//오류발생
}
{% endhighlight %}

3번째 줄에서 `cp` 문자열 변수를 일반 문자열 변수 `q`로 형변환 했다. 하지만, 4번째 줄 `const_cast<string>`은 자료형을 변환하는 것이기 때문에 오류가 발생한다.



[출처:최신 표준 C++로 쉽고 빠르게 안내하는 모던 C++ 프로그래밍]
