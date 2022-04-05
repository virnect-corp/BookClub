# EXERCISE 1.1

## Solved

|  |Code snippet 1|Code snippet 2|Code snippet 3|
|--|--------------|--------------|--------------|
|Are you retrieving knowledge from LTM?| No | Yes | Yes |
|If you are retrieving information from LTM, what information?| No | StringBuffer, reverse(), toString(), charAt() | INPUT LEN() FOR-TO-NEXT |
|Are you storing information in your STM?| Yes | Yes | Yes |
|What information are you storing explicitly?| function block, condition code | odd or even number branch, digit operator | RES$ reverse concat |
|What information are you ignoring because it seems irrelevant?| No | StringBuffer reverse | PRINT, LET RES$ |
|Is your working memory processing some parts of the code extensively?| Yes | Yes | No |
|Which parts of the code place a heavy load on your working memory?| ∇ keyword | for loop digit value | LET RES$=RES$&TX$(I), & operator and stack RES$ varialbe |
|Do you understand why these parts of code make the working memory work?| No | No | Yes |

### Code snippet 1: An APL program

What does this code do? What cognitive processes are involved?

함수를 구현한 코드, ⍵는 변수이고 1보다 작거나 같다면 어떤 연산을 수행함. 하지만 정확한 연산이 무엇인지는 파악하기 어려움

### Code snippet 2: A Java program

What does this code do? What cognitive processes are involved?

luhn algorithm test code. Java 코드를 알고 있으므로 적절한 LTM과 STM 과정이 일어남. 특히 comment 부분이 condition에 대한 이해를 도와주고 있음

### Code snippet 3: A BASIC program

What does this code do? What cognitive processes are involved?

string을 입력 받고 그걸 뒤집어서(reverse) 출력하는 프로그램, string의 Len연산, for loop, string concat 연산 등에 대한 문법 인지

## exercise 1.1

To practice your newly gained understanding of the three cognitive processes involved in programming, I’ve prepared three programs.
This time, though, no explanation is given of what the code snippets do. You
will, therefore, have to read the programs and decide what they do for yourself. The programs are again written in APL, Java, and BASIC, in that order.
However, each of the programs performs a different operation, so you cannot
rely on your understanding of the first program to support reading the other
programs.
Read the programs carefully and try to determine what they do. While doing
this, reflect on the mechanisms that you use. Use the questions in the following table to guide your self-analysis.

|  |Code snippet 1|Code snippet 2|Code snippet 3|
|--|--------------|--------------|--------------|
|Are you retrieving knowledge from LTM?| | | |
|If you are retrieving information from LTM, what information?| | | |
|Are you storing information in your STM?| | | |
|What information are you storing explicitly?| | | |
|What information are you ignoring because it seems irrelevant?| | | |
|Is your working memory processing some parts of the code extensively?| | | |
|Which parts of the code place a heavy load on your working memory?| | | |
|Do you understand why these parts of code make the working memory work?| | | |

### Code snippet 1: An APL program

``` APL
f • {⍵≤1:⍵ ⋄ (∇ ⍵-1)+∇ ⍵-2}
```

What does this code do? What cognitive processes are involved?

### Code snippet 2: A Java program

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

What does this code do? What cognitive processes are involved?

### Code snippet 3: A BASIC program

``` basic
100 INPUT PROMPT "String: ":TX$
120 LET RES$=""
130 FOR I=LEN(TX$) TO 1 STEP-1
140 LET RES$=RES$&TX$(I)
150 NEXT
160 PRINT RES$
```

What does this code do? What cognitive processes are involved?