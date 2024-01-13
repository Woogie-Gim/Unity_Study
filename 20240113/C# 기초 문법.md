# C# 기초 문법

## 상수와 열거형
- 기존에 작성한 가위바위보 게임은 하드코딩이기 때문에 유지보수측면에서 어려움이 있다.

- switch 문의 경우 상수 (고정된 변수)만 사용할 수 있다. 변동되는 값은 사용할 수 없다.
  
```C#
const int Rock = 0;
```
- 열거형은 메인 함수의 밖 클래스에서 선언해준다.

```C#
using System;

namespace Csharp
{
    enum Choice
    {
        Rock = 1,
        Paper = 2,
        Scissors = 0
    }

    class Program
    {
        static void Main(string[] args)
        {
            (int)Choice.Scissors;
        }
    }
}
```

- 열거형의 타입은 enum 타입이다. 형 변환을 해줘야 한다.

## while
- 반복의 의미를 가진다

```C#
using System;

namespace Chasrp
{
    class Program
    {
        static void Main(string[] args)
        {
            int cnt = 5;

            while (cnt > 0)
            {
                Console.WriteLine("Hello World!");
                cnt--;
            }
        }
    }
}
```

- while 문의 조건을 만족해야 while 문이 돌아간다. 즉, 거짓이 될 때까지 무한으로 돌아간다

- do while 문 : 우선 실행 후 while문을 체크해서 한번 더 들어올지 체크한다.

## for

- 반복문 / while문과 문법이 조금 다르다
- for (초기화식; 조건식; 반복식)

```C#
using System;

namespace Chasrp
{
    class Program
    {
        static void Main(string[] args)
        {
            for (int i = 0; i < 5; i++)
            {
                Console.WriteLine(i);
            }
        }
    }
}
```

## break, continue

- break의 경우 특정조건에서 반복문을 종료 해서 상위 반복문으로 바로 가게 해준다.
- continue의 경우 특정조건을 만족하지 못했을 때 다음 루프로 바로 가게 해준다.

## 함수

- 코드를 재사용할 수 있게 하나로 묶는 개념
- 무조건 클래스 안에서 선언해야 한다.
- 한정자 반환형식 이(매개변수 목록)
- 반환 형식이 없을 땐 void

### 반환 형식 없는 함수

```C#
using System;

namespace Chasrp
{
    class Program
    {
        static void HelloWorld()
        {
            Console.WriteLine("Hello World!");
        }
        static void Main(string[] args)
        {
            Program.HelloWorld();
        }
    }
}
```

### 덧셈 함수

```C#
using System;

namespace Csharp
{
    class Program
    {
        static int Add(int a, int b)
        {
            int result = a + b;
            return result;
        }
        static void Main(string[] args)
        {
            int result = Program.Add(4, 5);

            Console.WriteLine(result);
        }
    }
}
```

- 매개변수를 함수로 넘길 때 그냥 넘기게 될 경우 복사된 값으로 넘어가게 된다.
- ref 참조를 통해서 넘기게 될 경우 메모리 값을 넘기게 되어 정확히 그 값을 변화를 줄 수 있다.

```C#
using System;

namespace Csharp
{
    class Program
    {
        static void AddOne(ref int number)
        {
            number++;
        }
        static void Main(string[] args)
        {
            int a = 0;

            Program.AddOne(ref a);

            Console.WriteLine(a);
        }
    }
}
```

## ref, out

- 실제 연산 등에서는 ref를 사용하지 않고 int 함수 등을 사용하여 값을 변환하는데 값을 swap 하는 등의 경우엔 메모리를 직접 참조하여 변경하는 경우가 생긴다

- out을 사용해서 반환 하는 값을 여러 개를 반환할 수 있다. 대신 함수를 호출할 때 out을 사용한다는 것을 선언 해주어야 한다. (직접 메모리 값을 변환하기 때문)

```C#
using System;

namespace Csharp
{
    class Program
    {
        static void Divide(int a, int b, out int result1, out int result2) 
        {
            result1 = a / b;
            result2 = a % b;
        }
        static void Main(string[] args)
        {
            int num1 = 10;
            int num2 = 3;

            int result1;
            int result2;
            Divide(num1, num2, out result1, out result2);

            Console.WriteLine(result1);
            Console.WriteLine(result2);
        }
    }
}
```

## 오버로딩

- 과적하다 / 프로그래밍에서는 함수 오버로딩은 이름의 재사용
- 같은 이름을 사용하려면 매개변수 타입과 개수가 정확히 일치해선 안된다.

```C#
using System;

namespace Csharp
{
    class Program
    {
        static int Add (int a, int b)
        {
            Console.WriteLine("Add int 호출");
            return a + b;
        }

        static float Add (float a, float b)
        {
            Console.WriteLine("Add float 호출");
            return a + b;
        }
        static void Main(string[] args)
        {
            int ret = Program.Add(1, 2);
            Console.WriteLine(ret);

            float ret2 = Program.Add(2.2f, 3.2f);
            Console.WriteLine(ret2);
        }
    }
}
```