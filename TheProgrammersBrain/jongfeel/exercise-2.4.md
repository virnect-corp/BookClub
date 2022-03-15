# EXERCISE 2.4

Select a piece of code that is somewhat familiar to you. It can be something from your own codebase, or a small and simple piece of code from GitHub. It doesn’t matter all that much what code you select, or the programming language used. Something the size of half a page works best, and if possible, printing it on paper is encouraged.

Look at the code for a few seconds, then remove it from sight and try to answer the following questions:

* What is the structure of the code?

  – Is the code nested deeply or it is flat?

  – Are there any lines that stand out?

* How is whitespace used to structure the code?

  – Are there gaps in the code?

  – Are there large blobs of code?

**Answer**

Github에 있는 최근에 작성한 코드 기준으로 진행함. 오브젝트라는 책에서 영화 예매 프로그램 예제가 있는데 C#으로 다시 작성한 코드로 문제를 풀어봄. 아래는 코드 링크.

https://github.com/jongfeel/objects/blob/main/Chapter04/Movie/Movie.cs

### What is the structure of the code?

Movie class, 오버로딩 된 생성자들, 할인 조건에 대한 결과와 할인 가능한지 판단하는 몇 라인의 메서드.

#### Is the code nested deeply or it is flat?

class 한 개 짜리 코드라 nested한 코드는 없음 대체로 flat한 구조

#### Are there any lines that stand out?

할인 가능한지 여부를 체크하는 IsDiscountable() 메서드의 경우는 for문 안에 if문을 체크하는 구조로 되어 있어서 쉽게 눈에 들어오지 않았음

### How is whitespace used to structure the code?

C# 코드에 맞게 들여쓰기가 잘 되어 있었음

#### Are there gaps in the code?

역시 C# 코드에 맞게 간격이 잘 되어 있음. IDE에서 코드를 작성한 느낌이 많이 남

#### Are there large blobs of code?

크게 두 부분인데 빈 생성자 외에 생성자의 파라미터 값들을 일정하게 필드 변수에 저장하는 flat한 코드가 큰 덩어리였고

또 IsDiscountable() 메서드의 경우 for if 문의 코드로 구성되어 있다 보니 한 덩어리로 인식하게 됨