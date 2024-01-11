# C# 기초 문법

## if / else

```C#
using System;

namespace Csharp
{ 
    class Program
    {
        static void Main(string[] args)
        {
            int hp = 100;
            bool isDead = (hp <= 0);

            if (isDead)
            {
                Console.WriteLine("You are dead!");
            }
        }
    }
}
```
- 만약 if 조건을 만족하지 못한다면 else 구문으로 이동

## switch

- 반복을 방지하고자
- 정수랑 문자열을 넣을 수 있다
- switch - case - break
- default 아무것도 case에 해당하지 않으면 최종 default로
  
```C#
switch (choice)
{
    case 0:
        Console.WriteLine("가위 입니다.");
        break;
    case 1:
        Console.WriteLine("바위 입니다.");
        break;
    case 2:
        Console.WriteLine("보 입니다.");
        break;
    case 3:
        Console.WriteLine("치트키 입니다.");
        break;
    default:
        Console.WriteLine("다 실패했습니다.");
        break;
}
```

## 삼항 연산자

- bool _ = (조건 ? 맞을떄 : 틀릴떄);

```C#
int number = 25;

bool isPair = ((number % 2) == 0 ? ture : false);
```

## 가위-바위-보 게임

- 랜덤 함수를 사용하여 컴퓨터가 가위 바위 보를 내게 만들고 분기를 사용하여 가위 바위 보를 내게 한다

```C#
using System;

namespace Csharp
{
    class Program
    {
        static void Main(string[] args)
        {
            // 0: 가위, 1: 바위, 2: 보

            Random rand = new Random();
            int aiChoice = rand.Next(0, 3); // 0 ~ 2 사이의 랜덤 값

            Console.WriteLine("가위(0), 바위(1), 보(2) 중 하나를 선택하세요:");
            int choice = Convert.ToInt32(Console.ReadLine());

            switch (choice)
            {
                case 0:
                    Console.WriteLine("당신의 선택은 가위입니다.");
                    break;
                case 1:
                    Console.WriteLine("당신의 선택은 바위입니다.");
                    break;
                case 2:
                    Console.WriteLine("당신의 선택은 보입니다.");
                    break;
                default:
                    Console.WriteLine("잘못된 선택입니다. 가위(0), 바위(1), 보(2) 중 하나를 선택하세요.");
                    return;
            }

            switch (aiChoice)
            {
                case 0:
                    Console.WriteLine("컴퓨터의 선택은 가위입니다.");
                    break;
                case 1:
                    Console.WriteLine("컴퓨터의 선택은 바위입니다.");
                    break;
                case 2:
                    Console.WriteLine("컴퓨터의 선택은 보입니다.");
                    break;
            }

            // 승부 결정
            if (choice == aiChoice)
            {
                Console.WriteLine($"무승부입니다! 당신은 {GetHandName(choice)}를 선택하고, 컴퓨터는 {GetHandName(aiChoice)}를 선택했습니다.");
            }
            else if ((choice == 0 && aiChoice == 2) || (choice == 1 && aiChoice == 0) || (choice == 2 && aiChoice == 1))
            {
                Console.WriteLine($"승리입니다! 당신은 {GetHandName(choice)}를 선택하고, 컴퓨터는 {GetHandName(aiChoice)}를 선택했습니다.");
            }
            else
            {
                Console.WriteLine($"패배입니다! 당신은 {GetHandName(choice)}를 선택하고, 컴퓨터는 {GetHandName(aiChoice)}를 선택했습니다.");
            }
        }

        static string GetHandName(int hand)
        {
            switch (hand)
            {
                case 0:
                    return "가위";
                case 1:
                    return "바위";
                case 2:
                    return "보";
                default:
                    return "알 수 없음";
            }
        }
    }
}
```