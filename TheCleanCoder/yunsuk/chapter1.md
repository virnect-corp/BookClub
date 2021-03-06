# Bookclub

# ch1 프로의 마음 가짐

- 프로
- 책임감
    - 일정에 맞춘다는 이유로 테스트/확인이 되지 않은 것을 배포하는 것은 무책임 한 것이다.
    - 결국 다른 더 큰 피해를 가지고 오게 된다.
    - 힘든 결정이지만 책임감을 가지고, 제때 배포가 불가능하다는 것을 말하는게 옳다

## 기능에 해를 끼치지 마라

- 프로가되려면 오류를 만들면 안된다.
- 완벽할 순 없지만, 완벽하지 않아도 괜찮다가 아니다.
- 사과할 줄 알아야하고, 같은 오류를 반복하면 안되고, 경력을 쌓아가며 오류의 비율을 0에 가깝게 만들어야 한다.
- QA는 아무것도 찾지 못해야 한다.
    - 코드에 결함이 있지만 QA에 코드를 보내는 일은 프로답지 못함
        - 결함 - 확식을 갖지 못하는 코드
    - 잘돌아가는지도 모르는 코드를 QA에게 보내는 개발자는 프로가 아니다.
    - QA가 문제를 찾을 때 마다 다시는 그런 일이 생기지 않도록 마음을 다져야 한다.
- 제대로 작동하는지 아닌지 알아야 한다.
    - 테스트 또 테스트해야 한다. → 테스트를 자동화해야 하는 이유
    - 어떤 코드는 테스트하기 어렵다. → 테스트하기 쉽게 설계해야 한다. → 테스트 코드를 먼저 작성 TDD
- 자동화된 QA
    - 자동화 테스트만으로 출시 준비가 부족하긴 하지만, 최소한 시스템이 QA를 통과할 정도는 된다고 할 수 있다.

## 구조에 해를 끼치지 마라

- 전체 구조를 희생하면서 기능을 추가하는 것은 헛수고
- 구조가 좋아야 코드가 유연해진다
- 소프트웨어는 변한다가 기본 가정이고, 구조를 유연하게 만들지 못하면 경제 모델이 취약해진다.
    - ⇒ 비용을 치르지 않고 변경할 수 있어야 한다.
    - 형편 없는 구조 → 증가하는 공수, 개발자 고용, 상황은 더 악화,  구조에 더 큰 피해와 장애물 생성
- 소프트웨어 설계 원칙 패턴을 알아야 한다.
- 직접 바꿔보고 쉽지 않은지 확인해야 하기
    - 코드를 읽을 때마다 바꾸고 구조를 개선해야 한다.
    - 보이스카웃 규칙 - 코드를 볼때마다 착한 일을 하라
- 코드 바꾸기를 무서워 하는 이유 - 고장날까봐
    - ⇒ 자동화된 테스트가 필요한 이유
- 계속 바꾸고, 바꿔도 평안한 환경을 조성해야 한다. ⇒ 테스트 코드

## 직업윤리

- 자신의 경력을 회사에 맡기지 말아라
- 회사의 호의에 감사하라
- 한주에 60시간 계획을 짜고 20시간은 읽고 연습하고 공부하고 경력에 도움이 되는 공부를 해라
    - 하루에 3시간
    - 프로는 직업을 돌보는데 시간을 투자한다.
    - 열정을 강하게 만드는 일을 하라. 즐겁게 보내도록 하라.
- 전산 분야 지식을 익혀라
    - 바뀌지만 바뀌지 않는 것도 많다.
    - 최소한의 기술 목록
        - 디자인 패턴 : 24가지 GOF패턴, POSA 패턴을 실무에 적용할 수준
        - 설계원칙 : SOLID 객체 지향 원칙, 컴포넌트 개념
        - 방법론 : XP, 스크럼, 린, 칸반, 폭포수, 구조적 분석, 구조적 설계 개념
        - 원칙 : 테스트 주도개발, 객체지향 설계, 구조적 프로그래밍, 지속적 통합, 짝프로그래밍 실천
        - 도구 :  UML, 데이터 흐름도, 구조차트 , 흐름도 등..

## 끊임없이 배우기

- 코딩하지 않는 아키텍트는 NO
- 새언어를 배우지 않는 프로그래머 NO
- 새원칙과 기술 익히지 못한 개발자 NO
- 책, 기사, 블로그, 트윗, 컨퍼런스, 모임, 스터디 그룹, 낯선 것을 익혀라

## 연습

- 일상적인 업무는 연습이 아니다. 공연이다.
- 간단한 프로그래밍을 반복해서 하기
    - ⇒ 손가락과 두뇌를 훈련
    - 특정 리팩토링, 단축키 사용 능력 다듬기
    - 아침 10분, 저녁 10분

## 함께 일하기

- 함께 프로그래밍, 연습, 설계 계획에 노력

## 멘토링

- 배우기에 가장 좋은 방법은 가르치는 것
- 프로라면 후배를 멘토링하는 책임을 져야 한다.

## 업무지식을 익혀라

- 업무 분야의 책을 한두권 읽기
- 전문가와 시간을 보내고 대화를 나누자
- 사양에 오류가 있는지 알아보고 이의를 제기할 수 있을 만큼 업무를 알아야 한다.

## 회사와 고객에 동질감

- 문제를 이해하고 해결책을 만들기 위해 일해야 한다.
- 회사의 요구사항을 만족하는지 확인
- 개발자들끼리만 동질감을 가져선 안된다.

## 겸손

- 프로그래밍은 오만한 행위이다. 위험을 과감히 짊어진다.
- 실패한다. 사실과 위험 계산이 틀릴지도 모른다. 언젠가 내 능력이 부족해질 수 있다.
- 다른 사람을 비웃지 않고, 실수에 망신주지 않는다. 다음번에 실패할 사람은 자신이다.


이 챕터를 읽으며 가장 맘에 와닿고 담고 싶은 것은 '겸손'이었다.
비웃지 않고 망신 주지 않는다. 실패는 누구나 할 수 있다.

프로그래머는 본질적으로 이타적인 사람이 되어야 한다는 생각을 해본다.
함께 일하고, 해를 끼치지 않고, 친절해야 하고 이해시켜야 한다.