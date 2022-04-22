## Chapter 10 Estimation

## Discussions

챕터의 첫 두 페이지가 압박이 오는 상황에서 사람들에게 화를 내고 억지로 일을 시켰던 자신의 과거의 행동이 좋지 않다는 걸 일깨워주는 일화가 있습니다.
압박을 받는 상황이 있었다면 지금 상황에서 돌이켜 봤을 떄 그때의 심정과 지금 그 때를 생각했을때 심정이 어떤지를 얘기해 보면 좋을 것 같습니다.

### WHAT IS AN ESTIMATE ?

Business likes to view estimates as commitments(약속).
Developers like to view estimates as guesses(추측).

#### A COMMITMENT

약속을 했으면 그 약속을 존중해야 한다.
프로는 달성할 수 있다는 사실을 알지 못하면 약속하지 않는다. 아주 단순하다.

약속은 확실함에 관한 문제다.
다른 사람들은 당신의 약속을 받아들이고 거기에 기반해 계획을 짠다.

#### AN ESTIMATE

추정은 어림짐작이다. 약속은 포함되지 않는다. 아무런 약속(promise)도 하지 않는다.

```
의견)
그래서 commitment와 promise의 차이를 알아 보게 됐다.
commitment는 자신에 대한 약속이다. 즉 professionalism에 대한 것으로 스스로 언제 까지 할 수 있다 라는 믿음을 주는 의미이다. 
promise는 상대방에 대한 약속이다. 즉 trust에 대한 것으로 상대방에게 신뢰를 기반으로 뭔가를 해주겠다는 믿음을 주는 의미이다.

commitment는 한 sprint 내에서 자신이 언제 까지 이 일을 끝마칠 수 있다는 약속이고
promise는 사업부 사람에게 언제 까지 이 일을 끝마칠 수 있다는 약속이다.
```

불행히도 개발자들은 대부분 추정 실력이 형편없다.

```
의견)
개발자들의 추정의 의미는 가능성에 대한 의미는 맞는 것 같다.
3일 안에 끝낼 수 있는 확률이 50% ~ 60% 인건
책임이나 약속을 회피하기 좋은 핑계임에도 불구하고
이런 추정을 좋아하는 건 정말 좋은 핑계거리가 있기 떄문이라고 본다.
그건...

"해보지 않고는 알 수 없어요"
혹은
"해보고 나서 판단해야 알 수 있어요"

라는 점이다.

해봤는데 3일 만에 안된 건 50% ~ 60%의 확률에 들어가지 않은 것이므로
40% ~ 50% 확률로 안된 걸 대처하지 못한 사업부 사람들의 잘못으로 몰아가기가 너무 쉽다.

하지만, 개발자인 우리는 왜 사업부 사람을 힘들어 하는지 알고 싶다면
본인이 사업부 사람이 되면 알 수 있을 것이다.

확률적으로 일이 완료되는 걸 예측하면서 사업하는 걸 좋아하는 사람은 아무도 없다는 점을 생각해 보면
역으로 사업부 사람들에게 '언제까지 할 수 있어요?'라는 질문에 괴로워 해야 하는 것도 개발자가 감수해야 하는 것이라고 본다.
```

#### IMPLIED COMMITMENTS (엉겹결에 해버린 약속)

다른 해석의 여지가 없다.
'노력하겠다'의 동의는 '완료한다' 이다.
프로는 추정과 약속 사이에 명확한 선을 그어 구분짓는다.
프로는 확실히 성공한다는 사실을 알기 전에는 약속하지 않는다.

### PERT

PERT(Program Evaluation and Review Technique)는 미 해군이 폴라리스 잠수함 프로젝트를 지원하기 위해 만들었다.
PERT는 추정을 계산하는 방법을 포함한다.

프로 소프트웨어 개발자라면 빨리 끝내도록 노력해보라는 압박에도 불구하고 이성적인 예측을 하도록 매우 주의를 기울여야 한다.

```
의견)
PERT 기법에 대해서는 꼭 해야 하는가에 대해 의문을 품어볼 수 있지만
마지막에 이성적인 예측을 해야 한다는 점에서 주의를 해야 한다는 상당히 동의하는 편이다.

왜냐하면 개발자들은 추정치에 대한 예측이 형편 없기 때문에
대부분 사업부 사람들이 요구하는 특정 일정에 맞춰서
최대한 노력해서 일을 끝내야 할 수 밖에 없다(have to should be finished) 라는 상황을 잘 거부를 못하기 때문이다.

즉, 이성적으로 예측해도 안되는 걸 요구해도
'하다 보면 되겠지'
혹은
'될 때까지 하면 좋겠지'
라는 낙관적인 생각을 한다는 점이
개발자 스스로도 스트레스를 받는 덫에 뛰어는 것이고
사업부 사람도 나름 프로페셔널하지 못한 개발자와 일하는게 불만인
모두가 만족하지 못하는 일 처리가 되기 때문이다.
```

### ESTIMATING TASKS

추정에 사용하는 자원 중 가장 중요한 자원은 주변 사람들이다.
주변 사람들은 본인이 보지 못하는 것을 본다.
주변 사람들은 혼자서 추정하는 것보다 더 정확하게 추정할 수 있도록 도와준다.

#### WIDEBAND DELPHI

사람들을 모아 팀을 꾸리고,
업무에 대해 토론하고,
추정하고,
합의에 도달할 때까지 토론과 추정을 반복한다.

```
의견)
이런 방식에 매우 동의한다.

어떤 좋은 방법론 혹은 권력이 있는 특정 사람의 경험에 기반한 방법에 기대서
함께 일하는 사람들에게 지시 혹은 강요하는 방식으로
추정이 옳다고 주장하는 것은 상당히 좋지 않은 방법이라고 생각한다.
```

##### Flying Fingers

모두가 한 탁자에 둘러앉아 한 번에 하나의 업무에 대해서 토론.
필요한 것은 무엇인지, 혼란하거나 복잡하게 만들 일은 없는지, 어떻게 구현해야 할지를 토론.
업무가 얼마나 걸릴지를 0-5의 숫자로 손가락으로 표현.

동시에 손가락을 내미는게 중요한데, 다른 사람의 추정을 보고 판단하지 않기 위함.

##### Planning Poker

Flying fingers와 같은 방식, 대신 숫자가 적혀 있는 카드로 대체
마찬가지로 숫자의 의견이 일치하면 그 추정을 채택
아니라면 카드를 다시 가져와서 업무에 대해 토론을 계속 진행

##### Affinity Estimation (관계 추정)

모든 업무를 카드에 적되 추정 값은 적지 않는다.
더 긴 시간이 필요한 업무를 오른쪽을 옮긴다.
작은 업무는 왼쪽으로 옮긴다.

참여자는 다른 사람이 이미 옮긴 카드를 포함해 언제든 어떤 카드라도 옮길 수 있다.
어떤 카드를 특정 횟수만큼 이동했다면 토론을 위해 옆으로 빼 놓는다.

의견 불일치 카드에 대해 의견 합의를 위해 간단히 설계하는 시간을 가진다.

카드 뭉치 사이에 선을 그어 크기별로 구역을 구분한다.

##### Trivariate Estimates (3방 추정)

한 업무의 명목 추정 값을 선택하는 데 좋다. 세 추정 값으로 확률 분포를 만든다. 

### THE LAW OF LARGE NUMBERS

추정에는 오류가 가득하므로, 추정이라 부른다.
큰 업무를 여러 개의 작은 업무로 쪼개 따로따로 추정하면,
하나의 큰 업무 추정값보다 작은 업무들의 추정 값의 합이 정확하다는 게 이 법칙의 의미.