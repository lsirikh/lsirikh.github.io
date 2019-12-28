---
layout: single
title:  "07.C++ 변수와 자료형"
permalink: /categories/:categories/:title:output_ext
taxonomy: {title}
categories: C++
tags: C++ variables types
comments: true
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
<br>

## 1. 변수 설정

다양한 프로그램에서 변수는 필수적인 요소이다. 따라서, 그 의미는 설명할 필요가 없을 듯 하다.

```
int variable = 10;
```

variable라는 변수에 10이라는 상수를 저장하는 것을 볼 수 있다. 

변수를 설정하는 데 다음과 같은 몇 가지 유의사항이 있다.

* 의미를 파악할 수 있도록 식별할 수 있는 단어로 구성(가장중요)
* 일반적으로 소문자로 구성
* 클래스 이름은 일반적으로 대문자로 시작
* 숫자는 변수의 이름의 첫 글자로 사용할 수 없음
* 여러단어를 조합할 때는 일관성 있는 규칙을 적용할 것(예 student_score)
* 예약어는 변수의 이름으로 사용할 수 없다.


## 2. C++ 예약어

C++에서는 다음과 같은 예약어를 활용한다.

[그림]

## 3. C++ 기본 자료형

C++에서는 다음 기본 자료형을 활용한다.

[그림]

## 3. singed와 unsinged 타입

기본 자료형 중 숫자형 자료형은 다음과 같이 signed와 unsigned 타입을 갖게 된다.

```
long형의 (signed) 표현범위 : -2,147,483,648 ~ 2,147,483,648
long형의 unsinged 표현범위 : 0 ~ 4,294,967,295
```

## 4. 자료형 별칭 만들기

자료형에 의미있는 별칭(alias)를 모던 C++에서부터 가능해졌다.

```
1. typedef [기존 자료형] [별칭]
예) typedef double salary;
2. using [별칭] = [기존 자료형]; //C++11 표준 방식
예) using salary = double;
```


{% highlight c linenos %}
int main(){
    using salary = double; //double형에 salary라는 별칭을 선언
    using point = int; // int형에 point라는 별칭 선언

    //kiho 변수를 salary형으로 선언하고 값 할당
    salary kiho = 125.20;
    //wonbin 변수를 salary형으로 선언하고 값 할당
    salary wonbin = 100.12;

    return 0;
}
{% endhighlight %}


## 5. auto형 변수: 초깃값 필요

모던 C++11 부터 새롭게 적용된 타입이 중에 특이한 것이 바로 `auto` 타입이다. 
기존에는 데이터 타입을 정해서 메모리를 할당하고, 컴파일의 구분기준으로 활용하였으나, 
auto가 나오면서 이러한 방식을 자동으로 처리해주는 기능이 등장하게 되었다. 일종의 javascript에서 `var name`이라고 쓰고, 데이터를 할당해준 것과 다르지 않은 느낌이다.

```
auto 변수명 = 초깃값(상수, 변수, 함수 모두 가능);
```

{% highlight c linenos %}
{
    int n = 2;
    float f = 23.4;
    auto answer1 = n;
    auto answer2 = f;
    auto answer = n + f;
}
{% endhighlight %}

## 6. decltype형: 초깃값 불필요

모던 C++부터 지원하는 또 다른 타입은 decltype이다. auto형의 초깃값 불필요 버전이라고 볼 수 있을 것 같다.

```
1. decltype(함수 f()) [선언할 변수];
2. decltype(변수) [선언할 변수];
3. decltype((변수)) [선언할 변수];
```


{% highlight c linenos %}
int f(){
    return 20 + 30;
}

int main(){
    double d = 1.231;
    decltype(f()) answer1;  //1 번 내용
    decltype(d) answer2;    //2 번 내용
    decltype((d)) answer3 = answer2;  //3 번 내용
}
{% endhighlight %}


[출처:최신 표준 C++로 쉽고 빠르게 안내하는 모던 C++ 프로그래밍]
