# exercise 1.1

## APL

``` APL
f • {⍵≤1:⍵ ⋄ (∇ ⍵-1)+∇ ⍵-2}
```
LTM에서 관련된 지식을 인출 하는가? LTM에서 인출했다면, 어떤 정보를 가져왔는가?
- 수학기호 ≤ - + 

STM에 정보를 저장하는가? 구체적으로 어떤 정보를 저장하는가?
- 잘 모르겠음

관련이 없어 보여 무시하고 넘어가는 정보는 없는가?
- • 

코드의 특정 부분을 광범위하게 작업 기억 공간을 사용해서 분석하는가? 어떤 부분이 과부하를 주는가?
- 의미를 모르는 기호 ∇, ⋄

코드의 그 부분들이 작업 기억 공간을 어떻게 사용하는지 이해하는가?
- 기호의 의미가 어떤 것인지 몰라서 그 의미를 추론하려고 함

이 코드가 하는 일은 무엇인가? 어떤 인지 과정이 일어나는가?
- 변수⍵가 1이하일 때 수식에 따라 계산된 값을 결과값으로 반환하는 함수 f를 정의하는 것 같습니다.
- LTM에 의해 수학 기호가 쓰인 것을 보고 수학 수식을 표현하는 코드라고 파악. 낯선 기호 문법에 대한 정보가 LTM에 없어서 자세한 내용을 이해하지 못함.
- 찾아보니 피보나치 코드 인 것 같네요!? https://www.jsoftware.com/papers/tour_Bangalore/tourex_memo.htm


### Java

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
LTM에서 관련된 지식을 인출 하는가? LTM에서 인출했다면, 어떤 정보를 가져왔는가?
- 자바 키워드, 자료형 정보.

STM에 정보를 저장하는가? 구체적으로 어떤 정보를 저장하는가?
- number에 대입된 값, digit, s1, s2.

관련이 없어 보여 무시하고 넘어가는 정보는 없는가?
- StringBuffer, Luhn

코드의 특정 부분을 광범위하게 작업 기억 공간을 사용해서 분석하는가? 어떤 부분이 과부하를 주는가?
- s1과 s2에 대입되는 값. Character.digit

코드의 그 부분들이 작업 기억 공간을 어떻게 사용하는지 이해하는가?
- 루프가 돌 때마다 s1, s2에 저장되는 값을 기억하려고 함. 
- Character.digit라는 메소드가 숫자에 대한 처리를 하는 것 같은데 두번째 인자가 뭔지 모르겠어서 파악하려고 함.

이 코드가 하는 일은 무엇인가? 어떤 인지 과정이 일어나는가?
- 입력받은 숫자를 자리수에 따라 처리하여 true or false를 반환하는 것 같습니다. 
- LTM으로 키워드를 보고 자바 클래스와 메소드를 구현하는 코드라고 파악. STM을 이용하여 for 루프를 따라가며 이해하려고 시도하는데 부하가 걸려 자세한 동작을 파악하는 것은 포기하고 주석을 통해 대충 그렇구나 하고 이해하고 넘어감.
- 찾아보니 신용카드 번호 유효확인을 하는 알고리즘이네요! https://en.wikipedia.org/wiki/Luhn_algorithm 해당 알고리즘에 대한 정보가 LTM에 없어서 파악하기 어려웠던 것 같습니다.

## BASIC

``` basic
100 INPUT PROMPT "String: ":TX$
120 LET RES$=""
130 FOR I=LEN(TX$) TO 1 STEP-1
140 LET RES$=RES$&TX$(I)
150 NEXT
160 PRINT RES$
```
LTM에서 관련된 지식을 인출 하는가? LTM에서 인출했다면, 어떤 정보를 가져왔는가?
- for루프, print 키워드가 보이니 잘은 모르겠지만 프로그래밍 로직인 것 같기는 함.

STM에 정보를 저장하는가? 구체적으로 어떤 정보를 저장하는가?
- TX, RES

관련이 없어 보여 무시하고 넘어가는 정보는 없는가?
- 맨 왼쪽의 숫자. LET, $기호

코드의 특정 부분을 광범위하게 작업 기억 공간을 사용해서 분석하는가? 어떤 부분이 과부하를 주는가?
- TX, RES, for 루프문의 STEP-1. RES$&TX$(I)

코드의 그 부분들이 작업 기억 공간을 어떻게 사용하는지 이해하는가?
- 변수 이름이 무엇을 나타내는지 파악하려고 함. for 루프의 표현이 낯설어서 해석하려고 함. &와 (I)가 어떤 동작을 하는지 모르겠음

이 코드가 하는 일은 무엇인가? 어떤 인지 과정이 일어나는가?
- 입력받은 문자열의 글자를 거꾸로 출력하는 코드 인것 같습니다.
- LTM에 의해 Input, print 의 키워드를 보고 뭔가 입력을 받아서 출력에 반응하는 코드라고 판단. LTM에 문법 정보가 없어 for 루프의 표현을 해석하는데 작업기억 공간을 사용. 변수의 이름이 축약되어 있어 해석하는데 작업기억 공간을 사용.