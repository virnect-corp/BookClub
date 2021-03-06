# 배심원 등장

반복 시간을 줄이는 이상의 의미가 있다.

외과의사가 꼭 손을 싯어야 하듯이 프로그래머도 TDD를 적용해야 한다고 생각한다.

작성한 코드가 전부 잘 돌아가는지 알지 못한다면 어찌 프로라 말할 수 있겠나? 

# TDD의 세 가지 법칙

1. 실패한 단위 테스트를 만들기 전에는 제품 코드를 만들지 않는다.
2. 컴파일이 안되거나 실패한 단위 테스트가 있으면 더 이상의 단위 테스트를 만들지 않는다.
3. 실패한 단위 테스트를 통과하는 이상의 제품 코드를 만들지 않는다.

반복 주기는 30초 길이를 유지한다.

거듭해서 주기를 반복한다.

테스트 코드를 추가한다.

제품 코드도 조금 추가한다.

두가지 코드 흐름이 동시에 자라나 상호 보완하는 컴포넌트가 된다.

## 수많은 혜택

### 확신

제품을 출시할 정도로 충분한 확신 

### 결함 주입 비율

### 용기

나쁜 코드를 봐도 고치지 않을까? 

1. 정리좀 해야겠네
2. 안 건드릴 거야 

→ 나도 “안 건드릴 거야”에 속했다. 수정하다가 지금은 해당 코드를 발견하면 바로 수정은 하지 않고 깃헙 이슈를 생성하고 나중에 시간을 내어 수정하는 방식으로 바뀌었다.

TDD는 이러한 변경에 대한 두려움을 모두 사라지게 한다.

진정한 프로라면 제품이 계속 섞어가는데도 가만히 있을까?

### 문서화

단위 테스트는 문서다. 시스템의 가장 낮은 단계의 설계를 알려준다.

명확하고 정확하며 독자가 이해하는 언어로 만들어져 실행 가능한 형식을  갖춘다.

### 설계

테스트를 먼저 만들기 위해서는 좋은 설계를 고민해야한다.

세 가지 법칙에 따라 테스트를 먼저 만드는 일은 의존성이 낮은 좋은 설계를 만드는 힘이 된다.

먼저 만드는 테스트는 공격, 나중에 만드는 테스트는 수비이다.

사후 테스트는 먼저 만든 테스트만큼 예리하지 않다.

## 프로다운 선택

TDD는 프로다운 선택이다.

TDD 는 확신, 용기, 오류 감소, 문서화, 설계를 향상시키는 원칙이다.

# TDD와 관련 없는 사실

프로 개발자라면 좋은 점보다 해로운 점이 많을 대는 규칙을 따라서는 안 된다 

# 토론

제품을 출시할 정도로 충분한 확신이 든 경험이 있었나요? 전 없었습니다.