## 연습 문제 1번

- 장기 기억 공간 : LTM (지식이 없다)
- 단기 기억 공간 : STM (어떤 정보가 없다) -일시적으로 저장
- 작업 기억 공간 : 처리 능력의 부족

|  |코드 1|코드 2|코드 3|
|--|--------------|--------------|--------------|
|LTM에서 관련된 지식을 인출 하는가?| 아니오 | 네 | 네 |
|LTM에서 인출했다면, 어떤 정보를 가져왔는가?| 없음 | Lunh 클래스에서 메소드 luhnTest에 "49927398716"이라는 값을 넣어서 값을 구한다. | PRINT, String |
|STM에 정보를 저장하는가?| 네 | 네 | 네 |
|STM에 구체적으로 어떤 정보를 저장하는가?| f• :W ,◇,▽ | (s1+s2) % 10 == 0;,Character.digit | PROMPT, ":TX$, LET,RES$="",I=LEN(TX$) T0 1 STEP-1, LET RES$=RES$TX$(I), NEXT |
|관련이 없어 보여 무시하고 넘어가는 정보는 없는가?| 아니오 | 아니오 | 아니오 |
|코드의 특정 부분을 광범위하게 작업 기억 공간을 사용해서 분석하는가?| 네 | 네 | 네 |
|코드의 어떤 부분이 작업 기억 공간에 과부하를 주는가?| f• :W ,◇,▽ | luhnTest method 내용들 | PROMPT, ":TX$, LET,RES$="",I=LEN(TX$) T0 1 STEP-1, LET RES$=RES$TX$(I) |
|코드의 그 부분들이 작업 기억 공간을 어떻게 사용하는지 이해하는가?| 아니오 | 네 | 아니오|

1번 코드
``` APL
f • {⍵≤1:⍵ ⋄ (∇ ⍵-1)+∇ ⍵-2}
```

- 이 코드가 하는 일은 무엇인가? 어떤 인지 과정이 일어나는가?
w가 1이하 인 경우에 조건이 w-1 + w-2를 하는 것 같습니다.
작업 기억 공간에 처리 능력이 부족하여 과부화 현상이 발생하는 거 같습니다.

2번 코드
``` java
public class Luhn {
    public static void main(String[] args) {
        System.out.println(luhnTest("49927398716"));
    }
    
    public static boolean luhnTest(String number) {
        int s1 = 0, s2 = 0;
        String reverse = new StringBuffer(number).reverse().toString();
        for (int i = 0; i < reverse.length(); i++) {
            int digit = Character.digit(reverse.charAt(i), 10);
            if (i % 2 == 0) { //this is for odd digits
                s1 += digit;
            } else { //add 2 * digit for 0-4, add 2 * digit - 9 for 5-9
                s2 += 2 * digit;
                if (digit >= 5) {
                    s2 -= 9;
                }
            }
        }
        return (s1 + s2) % 10 == 0;
    }
}
```
- 이 코드가 하는 일은 무엇인가? 어떤 인지 과정이 일어나는가?
LunhTest 라는 메서드를 출력해주는 코드, 단기 기억 공간에 처리하는 것 같습니다.

3번 코드
``` basic
100 INPUT PROMPT "String: ":TX$
120 LET RES$=""
130 FOR I=LEN(TX$) TO 1 STEP-1
140 LET RES$=RES$&TX$(I)
150 NEXT
160 PRINT RES$
```

- 이 코드가 하는 일은 무엇인가? 어떤 인지 과정이 일어나는가?
문자열을 출력하는 코드 같습니다. 작업 기억 공간에 잘 모르는 문법이라 과부화 현상이 발생하는 것 같습니다.