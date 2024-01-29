# region

- 말 그대로 코드를 지역별로 깔끔하게 나누는 것을 의미
- region을 사용하여 비슷한 코드끼리 묶어 가독성을 높여줄 수 있다
- 코드가 길어질 경우 다른 코드들을 배제하면 그 코드에만 집중할 수 있도록 도와준다

## region 사용 방법

- 감싸줄 코드의 시작과 끝에 #region과 #endregion을 붙여준다
- #region과 #endregion의 옆에는 코멘트를 달아서 #region을 접은 경우에도 코멘트를 언제든지 확인할 수 있다

```C#
#region 리전을 시작합니다
string a;
string b;
string c;
#endregion 리전을 종료합니다
```

## 주의 사항
- 너무 남발하는 경우 가독성이 떨어진다