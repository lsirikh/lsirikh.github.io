---
layout: single
title:  "08.C++ 트위터 연동 주소록 관리 프로젝트01"
permalink: /categories/:categories/:title:output_ext
taxonomy: {title}
categories: C++
tags: C++ twitter project01
comments: true
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
<br>

## 1. 트위터 연동 주소록 관리 프로젝트 ADT

이 프로젝트는 다음과 같은 항목과 기능으로 구성된 프로젝트 이다. 책속에 진행하는 프로젝트라서 프로그래밍 언어를 학습하는 가장 좋은 방법은 프로젝트라고 개인적으로 믿고 있기 때문에 단편적으로 학습한 항목별 지식은 통합되기 매우 어렵다고 생각한다.
따라서, 힘들 수 있지만, 지식의 통합과정은 개별지식을 심화시키기도 하며, 본인의 역량을 강화하는 아주 좋은 수단이 된다고 본다.

[그림]

## 2. 이번 프로젝트 단위에서 제작된 코드



{% highlight c linenos %}
#include <iostream>

using namespace std;

struct OwnerInfo {
	char name[20];			//이름
	char phoneNumber[13];	//전화번호
	char email[30];			//이메일
	char address[100];		//주소
	char twitterAccount[20];		//트위터 계정
};

struct ContactInfo {
	char name[20];			//이름
	char phoneNumber[13];	//전화번호
	char email[30];			//이메일
	char address[100];		//주소
};

//전역변수 할당
OwnerInfo owner;
ContactInfo contacts[100];
int contactNumber = 0;

void inputOwnerInfo() {

	cout << "소유자 이름: ";
	cin >> owner.name;

	cout << "소유자 전화번호: ";
	cin >> owner.phoneNumber;

	cout << "소유자 이메일: ";
	cin >> owner.email;

	cout << "소유자 주소: ";
	cin >> owner.address;

	cout << "소유자 트위터 계정: ";
	cin >> owner.twitterAccount;

	cout << "입력이 완료 되었습니다.";
}

void outputOwnerInfo() {
	cout << "소유자 이름: " << owner.name << endl;
	cout << "소유자 전화번호: " << owner.phoneNumber << endl;
	cout << "소유자 이메일: " << owner.email << endl;
	cout << "소유자 주소: " << owner.address << endl;
	cout << "소유자 트위터 계정: " << owner.twitterAccount << endl;

}

void addContact() {
	cout << "연락처 이름: ";
	cin >> contacts[contactNumber].name;

	cout << "연락처 전화번호: ";
	cin >> contacts[contactNumber].phoneNumber;

	cout << "연락처 이메일: ";
	cin >> contacts[contactNumber].email;

	cout << "연락처 주소: ";
	cin >> contacts[contactNumber].address;

	contactNumber++;
	cout << "입력이 완료 되었습니다." << endl;
}

void outputContactList() {
	int i;

	for (i = 0; i < contactNumber; i++) {
		cout << i << " : " << contacts[i].name << endl;
	}

}

void runOwnerMenu(); //선언
void runContactMenu();//선언

void runMainMenu() {

	int menuNum;

	do {
		cout << "1. 소유자 관리 기능" << endl;
		cout << "2. 연락처 관리 기능" << endl;
		cout << "3. 프로그램 종료" << endl;
		cout << ">";
		cin >> menuNum;

		switch (menuNum) {
		case 1:
			runOwnerMenu();
			break;
		case 2:
			runContactMenu();
			break;
		case 3:
			cout << "프로그램을 종료 합니다." << endl;
			break;
		default:
			cout << "잘못 입력 하셨습니다. 다시 해주세요." << endl;

		}
	} while (menuNum != 3);

}

void runOwnerMenu() {
	int menuNum;

	do {
		cout << "1. 소유자 정보 입력" << endl;
		cout << "2. 소유자 정보 조회" << endl;
		cout << "3. 이전 화면" << endl;
		cout << ">";
		cin >> menuNum;

		switch(menuNum){
		case 1:
			inputOwnerInfo();
			break;
		case 2:
			outputOwnerInfo();
			break;
		case 3:
			cout << "이전 화면으로 돌아 갑니다." << endl;
			break;
		default:
			cout << "잘못 입력 했습니다. 다시 해주세요." << endl;
		}
	}while(menuNum !=3);
}

void runContactMenu(){
	int menuNum;

	do{
		cout << "1.연락처 추가 입력" << endl;
		cout << "2.연락처 조회" << endl;
		cout << "3.이전 화면" << endl;
		cout << ">";
		cin >> menuNum;

		switch(menuNum){
		case 1:
			addContact();
			break;
		case 2:
			outputContactList();
			break;
		case 3:
			cout << "이전 화면으로 돌아 갑니다." << endl;
			break;
		default:
			cout << "잘못 입력 했습니다. 다시 해주세요." << endl;

		}
	}while(menuNum !=3);
}


int main(){
	runMainMenu();

	return 0;
}

{% endhighlight %}


[출처:최신 표준 C++로 쉽고 빠르게 안내하는 모던 C++ 프로그래밍]
