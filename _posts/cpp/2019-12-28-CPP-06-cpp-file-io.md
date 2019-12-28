---
layout: single
title:  "06.C++ 파일 입출력"
permalink: /categories/:categories/:title:output_ext
taxonomy: {title}
categories: C++
tags: C++ file IO
comments: true
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
<br>

## 1. 파일 입출력

파일 입출력은 말 그대로, 파일 형태로 데이터를 입출력 하는 라이브러리를 사용하는 방법을 살펴본다.

* 필요한 라이브러리 헤더 fstream(파일클래스)
* 네임스페이스 std(표준 라이브러리)

{% highlight c linenos %}

#include <fstream>
#include <iostream>
#include <string>

using namespace std;

int main(){
	string str = "안녕하세요.글자를써봅시다.";

	ofstream ofs("file.txt"); //file.txt 파일을 연다.
	ofs << str; // file.txt 파일에 str 문자열을 쓴다.
	ofs.close(); //file.txt를 닫는다.
	ifstream ifs("file.txt"); //file.txt 파일을 다시열고,
	ifs >> str; //파일의 내용을 str에 저장한다.
	str = str+"(읽어옴.)";
	cout << str << endl;
	return 0;

}
{% endhighlight %}

이 코드를 실행하면, file.txt 파일이 프로젝트 폴더에 생성되고, 결과는 다음과 같이 나온다.

```
안녕하세요.글자를써봅니다.(읽어옴.)
```

하지만, 주의할 점은 띄어쓰기를 하면 이상하게 출력될 수 있다는 점을 확인하기 바란다.

```
출력 : ofstream → fstream(ios::out);
입력 : ifstream → fstream(ios::in);
```
<br>
* 파일 모드 표

|파일 모드| 설명 |
|---
|ios::in|파일 읽기|
|ios::out|파일 쓰기|
|ios::app|파일에 이어쓰기(마지막 줄부터)<br>예)fstream(ios::app)와 같이 ios::out과 함께 써야 함.|
|ios::trunc|파일이 이미 있으면, 삭제하고 새로 파일 작성<br>예) 파일 읽을 때: fstream(ios::in\|ios::trunc)<br>예) 파일 쓸 때:fstream(ios::out\|ios::trunc)|
|ios::binary|이진 파일 처리<br>예) 파일 읽을 때: fstream(ios::in\|ios::binary)<br>예) 파일 쓸 때: fstream(ios::out\|ios::binary)|

<img src="/assets/img/" title="">



{% highlight c linenos %}

#include <fstream>

using namespace std;

int main(){

	ofstream ofs;

	//file.txt 파일을 연다.(없으면 생성)
	ofs.open("file.txt");

	//"This is an apple" 문자열을 쓴다.
	ofs.write("This is an apple", 16);

	//tellp() 멤버함수를 이용해서 파일의 현재 위치를 얻는다.
	// 현재위치는 This is an apple의 맨 끝일 것이다.
	long pos = ofs.tellp();

	//현재 위치에서 7만큼 위치를 뒤로 이동시킨다.
	//현재 위치를 앞뒤로 조정하는 것을 오프셋(offset)을 조정한다고 한다.
	//오프셋 -7로 조정한 위치는 문자 'n'이다.
	ofs.seekp(pos-7);

	//조정한 위치부터 문자열 "sam" 을 쓴다.
	ofs.write(" sam", 4);

	//파일을 닫는다.
	ofs.close();

	return 0;

}
{% endhighlight %}


[출처:최신 표준 C++로 쉽고 빠르게 안내하는 모던 C++ 프로그래밍]
