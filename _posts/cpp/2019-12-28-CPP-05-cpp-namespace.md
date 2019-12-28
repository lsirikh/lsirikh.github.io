---
layout: single
title:  "05.C++ 네임스페이스(namespace) 사용하기"
permalink: /categories/:categories/:title:output_ext
taxonomy: {title}
categories: C++
tags: C++ 네임스페이스 namespace
comments: true
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
<br>

## 1. 네임스페이스

C++에서 가장 먼저 접하게 되는 개념이 바로 네임스페이스다. 
처음 Hello Wordl를 출력할 때, 의미도 모른채 `using namespace std`를 쓴 기억이 있을 것이다.

네임스페이스는 단어 그래도 지정한 라이브러리를 사용할 수 있도록 소속을 알리는 역할을 한다.

{% highlight c linenos %}
using namespace std;
{% endhighlight %}

이렇게 사용하게 되면, std라는 라이브러리가 더 이상 소속과 기능을 같이 쓰지 않아도 된다. 이게 무슨말이냐하면,


{% highlight c linenos %}
//일반적을 namespace를 선언 안한 경우
#include <iostream>

int main(){

    std::cout << "Hello Wolrd" << endl;
    return 0;
}
{% endhighlight %}


## 2. 네임스페이스 범위 지정에 따른 차이비교

* using namespace std 경우

{% highlight c linenos %}
#include <iostream>

using namespace std;

int main()
{
    int i = 0;
    cin >> i; //숫자 키보드 입력받기
    cout << i; //입력 받은 숫자를 화면에 출력하기
    return 0;
}
{% endhighlight %}


* using namespace std의 부분을 설정한 경우

{% highlight c linenos %}
#include <iostream>

using std::cout; //cout으로 범위를 좁혀서 namespace 지정

int main()
{
    int i = 0;
    cin >> i; //컴파일 오류 발생
    std::cin >> i; //정상적으로 실행 가능한 코드
    cout << i; //입력 받은 숫자를 화면에 출력하기
    return 0;
}
{% endhighlight %}


두 코드에서 알 수 있듯이, namespace는 범위를 지정해서 사용할 수 있고, 범위를 지정하면 다른 라이브러리의 다른 기능을 사용할 때 선별적으로 접근 할 수 있다.

## 3. namespace 직접 정의


```
namespace 네임스페이스명
{
    선언 내용:(클래스, 함수, 변수 등을 정의)
}
```


이와 같은 방식으로 namespace를 지정 할 수 있다.

* 변수를 사용한 네임스페이스 설정

{% highlight c linenos %}
#include <iostream>

using namespace std;

//first 네임스페이스 정의
namespace first
{
    int value = 1;
}

//second 네임스페이스 정의
namespace second
{
    int value = 2;
}

int main()
{
    cout << first::value; // 1을 출력
    cout << second::value; // 2를 출력

    return 0;
}
{% endhighlight %}


[출처:최신 표준 C++로 쉽고 빠르게 안내하는 모던 C++ 프로그래밍]
