# C# 기초 프로그램 입문

## 기본 틀

```C#
using System;

// 프로젝트 명
namespace Csharp
{ 
    class Program
    {
        static void Main(string[] args)
        {

        }
    }
}
```

## 데이터 형식
- 데이터를 다룰 때는 어떠한 형식의 데이터를 결정하고 데이터를 다룬다

### 대표적 데이터 형식
- int : 정수형
- float : 실수형
- string : 문자열
- bool : 참과 거짓

- 사용빈도가 가장 높은 건 정수형 자료

## 변수
- 타입에 따른 변수를 할당한다
- 메모리에 변수가 저장되고 컴파일 된다
- 할당된 변수에 데이터를 쓰고 저장한다
- [데이터타입] [이름];
```C#
int hp;
hp = 100;

int maxHp = hp;
```

## 정수 형식
- long int의 범위는 -2,147,483,648 ~ 2,147,483,648
  
## 2진수, 10진수, 16진수
- 컴퓨터 같은 경우 모든 경우를 0과 1로 표현한다
- 10진법 : 1 2 3 4 5 6 7 8 ...
- 2진법 : 0b00 0b01 0b11 ...
- 16진법 : 0 1 2 3 4 ... 7 8 9 10 A B C D E F
  
```C#
int hp = 0x12FB2;
```
- 비트 연산 등에서 진수별로 사용하기도 한다

## 정수 범위의 비밀

![Alt text](<Images/정수 범위.PNG>)
- Signed : 부호가 있는 수
- UnSigned : 부호가 없는 수

- 최상위 비트는 음수를 표현하는데 사용한다 (2의 보수법)
- 부호가 없을 경우 최상위 비트를 사용하더라도 부호가 바뀌지 않는다

![Alt text](<Images/2의 보수법.png>)

## float

![Alt text](<Images/실수 범위.PNG>)

```C#
float a = 3.14f;
```
- f가 붙어야만 실수형 타입으로 인식을한다
- 무한대로 소수점을 붙일 수 없기 떄문에 정확히 일치하지 않게 컴퓨터가 수정할 수 있다 (근사값)
- 근사값이기 때문에 float형은 권장되지 않는다

```C#
double b = 3.5;
```
- double은 메모리를 float보다 2배 차지하는 대신 정밀하게 계산 해준다

## string

```C#
string name = "hi";
```

```C#
char ch = 'R';
```

- string 문자열 "";
- Character 타입은 문자 '';
- C# 에선 char 타입은 2바이트 C++ 에선 1바이트

## bool

```C#
bool a = true;
bool b = false;
```

- true와 false 두 가지만 표현하지만 중요도는 정수형 문자열 등과 같다
- 예를 들어 운영자를 표현하기 위해 isAdmin bool 타입을 통해서 구분할 수 있다

## 캐스팅

- 형식 변환
```C#
int a = 100;
short b = a;
```
- 직접 변환을 하려고 할 경우 큰 곳에서 작은 곳 4바이트에서 2바이트로 옮기려고 하면 에러 발생

```C#
int a = 100;
short b = (short)a;

float c = a;
int d = (int)c;
```
- 단 작은 곳에서 큰 곳으로 옮길 경우 short에서 담기는 변수는 int에서도 당연히 담기기 때문에 에러가 나지 않는다

## 스트링 포맷

- ConSole.WriteLine(); 출력 (cout)
- Console.ReadLine(); 입력 (cin)

```C#
string input

input = Console.ReadLine();

Console.WirteLine(input);
```

- 파싱
  
```C#
string input = Console.ReadLine();

int number = int.Parse(input);

Console.WirteLine(number);
```

- 다양한 형 출력하기
  
```C#
int hp = 100;
int maxHp = 100;

// 옛날 방법
string.Format("당신의 HP는 {0}/{1} 입니다.", hp, maxHp);

// String interpolation
string message = $"당신의 HP는 {hp}입니다.";
Console.WriteLine(message);
```

## 산술 연산
- 사칙 연산
- '+ '-' '*'' '/' '%'
- % : 모듈러 연산(나머지 연산)
- 우선순위가 존재
- 연산 순서는
  1) 할당 / int hp;
  2) write / hp = 100;
  3) read / hp;

- 나누기 연산은 데이터 형에 따라 몫을 나타내줌

- 증감연산
```C#
a += 1;
a++;

b -= 1;
b--;

++a;
--b;
```

- 전위 연산은 연산의 우선순위가 먼저 / 후위 연산은 연산의 우선순위가 뒤로

## 비교연산
- < <= > >= == !=
- 크다 크거나 같다 작다 작거나같다 같다 다르다

- true or false로 return (boolean으로 return)

## 논리연산
- 조건 여러개를 혼합해서 볼 경우 등에서 사용
- AND OR NOT
- && || !
- && 연산은 둘 다 만족해야 만족한다
- || 둘 중 하나라도 만족하면 만족한다