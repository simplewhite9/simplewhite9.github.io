---
title:  "클래스 & 생성자, 소멸자"
categories: [C++ 정복]
tags : [Class, constructor, deconstructor]
thumbnail-url: /assets/img/thumbnail/C.png
description: C++ OOP의 key "class"와 생성자 연산자에 관한 내용 정리

---

<div class="post-subtitle">구조체 (Structure)</div>

먼저 C++에서도 구조체를 사용 할 수 있다

```cpp
#include <iostream>
#include <string>

using namespace std;

//구조체 정의
struct person{
	string name;
	int age;
},

int main(void){
	struct person a;
	a.name = "Joseph";
	a.age = 23;
	...
}
```
<br>

<div class="post-subtitle">Class 클래쓰</div>

Object oriented programming에서 사용되는 class

---
<br>
`public`, `private`, `protected` 로 나누어서 설정이 가능하다

(1) `public`: 어디에서나 접근이 가능함 (주로 method)

(2) `private`: class 내부의 함수로만 접근이 가능함 (기본적으로 member는 private)

(3) `protected` : 상속 관계에서만 접근이 가능함

---
<br>
**Characteristics of C++(OOP) class**

1. Abstract
2. Encapsulation
3. Inheritance
4. Data Hiding
5. Polymorphism

---
<br>
```cpp
class people {

private:
	//Member 변수
	string name;
	int age;

public:	
	//Method 

	//constructor
	People(string n, int a) { 
			name = n; age = a;
	}

	void show() {
		 cout << name << " : " << age << "살\n";
	}
};

int main(void){
	People a = People("Emily", 22);
	a.show();
}
```

> Constructor를 통해 instance를 생성

<br>

**Data Hiding**을 활용한 예시

```cpp
class Student {

private:
	string name;
	int engScore;
	int mathScore;

	int getScore() { 
		//prviate에 정의해 Data Hiding
		return engScore + mathScore;
	}

public:
	Student(string n, int e, int m){
		name = n;
		engScore = e;
		mathScore = m;
	};

	void Show() {
		cout << name << " : [총점 " << getScore() << "점]\n";
	}

};

int main(void){
	Student a = Student("Emily", 85, 90);
	a.show();

	//cout << a.getScore();
	//위와 같이 getScore를 호출할경우 ERROR 발생 (private)
}
```

> *OUTPUT*: Emily : [총점 175점]

<br>

**this 포인터 활용하기**

```cpp
//constructor에서
...
public:
	Student(string n, int e, int m){
		name = n;
		engScore = e;
		mathScore = m;
	};
...
```

위 생성자 같은 경우 class 멤버 변수 이름과 생성자에서 사용되는 변수 이름이 다르다<br>
그래서 `name`  = `n` 이라고 적어도 `name` 이 `Student` 클래쓰의 멤버 변수를 뜻한다는 것을 바로 알 수 있다

하지만 위와 같은 경우가 아닐때는 `this`를 활용해야한다

```cpp
...
public:
	Student(string name, int engScore, int mathScore){
		//name = name ( 오류 발생 )
		this->name = name;
		this->engScore = engScore;
		this->mathScore = mathScore;
	};
...
```

> `this->` 를 활용해서 현재 해당 함수를 호출한 instance의 멤버 변수 `name`에 함수에 argument로 들어온 `name` 값을 입력할 수 있다
> 

<br>

<div class="post-subtitle">Constructor & Deconstructor</div>

**Constructor**:

1. 객체를 초기화하는 함수
2. Class 이름과 동일한 이름
3. 변환 return 값이 없다

**참고**: Constructor를 구현하지 않은 경우 Member 변수들은 0, NULL 값으로 자동으로 초기화 된다

<br>

**Copy Constructor**:

다른 instance의 reference를 인수를 받아 자신의 instance를 초기화하는데 활용한다<br>
다만 복사 생성자는 기존의 인스턴스의 다른 메모리 공간에 할당(deep copy를 통해 복사)되기 때문에 독립성을 갖도록 해줍니다

```cpp
...
public:
	//기본 constructor를 짧게 쓰는 방법
	Student( string name, int engScore, int mathScore) : 
            name(name), engScore(engScore), mathScore(mathScore) { }
	
	//Copy Constructor ( other를 받는다)
	Student(const Student& other){
		name = other.name;
		engScore = other.engScore;
		mathScore = other.mathScore;
	}
...

int main(void){
	//기존 constructor로 instance 생성
	Student student1("Emily", 95, 100);

	//Copy constructor로 instance 생성
	Student student2(student1);
}
```

> Student1을 이용해서 student2를 만들어낸다

<br>

**Deconstructor**:

1.  객체를 제거하는 목적으로 사용 (보통 동적 할당 인스턴스의 경우 활용)
2.  Class 이름과 동일한 이름을 사용하지만 물결을 이용해서 구별

```cpp
...
public:
	Student( string name, int engScore, int mathScore) : 
            name(name), engScore(engScore), mathScore(mathScore) { }
	
	//소멸자
	~Character() {
		cout << "Delete instance \n";
	}

...

int main(void){
	//동적 할당으로 student1 생성
	Student* student1 = new Student("Emily", 90, 100);
	Student student2(*student1);
	
	delete student1; //소멸
	delete &student2; //동적 할당으로 생성되지 않았기 때문에 제거되지 않는다
}
```

<br>