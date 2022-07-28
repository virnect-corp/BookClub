## Chapter 08 Moving Features

### Discussion

특별히 논의 내용이 없을 것으로 예상됐으나...

`8.8 반복문을 파이프라인으로 바꾸기` 에 대해서 어떻게 생각하는지 얘기를 해보면 좋을 것 같습니다.

어떤 사람은 문법이 어려우니까 쉬운 문법을 써야 한다면 for loop + if문을 사용하는 걸 선호하는 분도 있고\
map, filter 등의 파이프라인으로 하는게 동작이 같고 코드의 양도 줄면서 언어 혹은 프레임워크에서 지원하는 문법이니까 사용하는게 좋다는 분도 있습니다.

어떤 걸 더 선호하시나요?\
리팩터링에서 파이프라인 함수를 사용하는 걸 권장하는 걸 보면 쓰는게 맞는 거 같습니다.

### 8.1 Move Function

1판에서의 이름: 메서드 이동

``` javascript
class Account {
    get overdraftCharge() { ... }
}
```

=> 

``` javascript
class AccountType {
    get overdraftCharge() { ... }
}
```

#### 배경

좋은 소프트웨어 설계의 핵심: 모듈화가 잘 되어 있느냐를 뜻하는 모듈성(modularity)
프로그램 어딘가를 수정하려 할 때 해당 기능과 깊이 관련된 작은 일부만 이해해도 가능하게 해주는 능력
프로그램에 대한 이해도가 높아질수록 소프트웨어 요소들을 더 잘 묶는 새로운 방법을 깨우치게 뒨다.

객체지향 프로그래밍의 핵심 모듈화 컨텍스트는 클래스다.

함수들을 한 컨텍스트에 두고 작업해 보면 좋다. 그곳이 얼마나 적합한지는 차차 깨달아가게 되고 잘 맞지 않는다고 판단되면 위치를 옮기면 된다.

#### 절차

- 선택한 함수가 현재 컨텍스트에서 사용 중인 모든 프로그램 요소를 살펴본다. 이 요소들 중에도 함께 옮겨야 할 게 있는지 고민해본다.
- 선택한 함수가 다형 메서드인지 확인한다
- 선택한 함수를 타깃 컨텍스트로 복사한다(이때 원래의 함수를 소스 함수(source fucntion)라 하고 복사해서 만든 새로운 함수를 타깃 함수(target function)라 한다). 타깃 함수가 새로운 터전에 잘 자리 잡도록 다듬는다.
- 정적 분석을 수행한다.
- 소스 컨텍스트에서 타깃 함수를 참조할 방법을 찾아 반영한다.
- 소스 함수를 타깃 함수의 위임 함수가 되도록 수정한다.
- 테스트한다.
- 소스 함수를 인라인할지 고민해본다.

#### 예시: 중첩 함수를 최상위로 옮기기

GPS 추적 기록의 총 거리를 계산하는 함수

#### 예시: 다른 클래스로 옮기기

은행 이자 계산 bankCharge(), 초과 인출 이자 계산 overdraftCharge() 등의 함수 옮기기

### 8.2 Move Field

``` javascript
class Customer {
    get plan() { return this._plan; }
    get discountRate() { return this._discountRate; }
}
```

=>

``` javascript
class Customer {
    get plan() { return this._plan; }
    get discountRate() { return this.plan_discountRate; }
}
```

#### 배경

프로그램의 상당 부분이 동작을 구현하는 코드로 이뤄지지만 프로그램의 진짜 힘은 데이터 구조에서 나온다. 주어진 문제에 저합한 데이터 구조를 활용하면 동작 코드는 자연스럽게 단순하고 직관적으로 짜여진다.

```
프로그래밍을 많이 하다 보니 위 문장의 말이 어느 정도 와 닿는 부분이 많다. 잘못된 자료 구조가 코드 로직을 직관적이지 못하게 만드는 부분이 분명히 있다.
```

경험과 도메인 주도 설계 같은 기술이 데이터 구조를 설계하는데 도움이 된다. 하지만 초기 설계는 실수가 많은데 프로젝트가 진행될수록 문제 도메인과 데이터 구조가 계속 변경될 수 밖에 없는 변화를 겪기 때문이다.

데이터 구조가 적절치 않음을 깨닫게 되면 곧바로 수정한다.

함수에 어떤 레코드를 넘길 때마다 또 다른 레코드의 필드도 함께 넘기고 있다면 데이터 위치를 옮겨야 한다. 한 레코드를 변경하려 할 때 다른 레코드의 필드까지 변경해야만 한다면 필드의 위치가 잘못되었다는 신호다. 레코드 대신 클래스나 객체가 와도 똑같다.

#### 절차

- 소스 필드가 캡슐화되어 있지 않다면 캡슐화한다.
- 테스트한다.
- 타깃 객체에 필드(와 접근자 메서드들)를 생성한다.
- 정적 검사를 수행한다.
- 소스 객체에서 타깃 객체를 참조할 수 있는지 확인한다.
- 접근자들이 타깃 필드를 사용하도록 수정한다.
- 테스트한다.
- 소스 필드를 제거한다.
- 테스트한다.

#### 예시

고객 클래스(Customer)와 계약 클래스(CustomerContract)

#### 예시: 공유 객체로 이동하기

### 8.3 Move Statements into Function (문장을 함수로 옮기기)

반대 리팩터링: 문장을 호출한 곳으로 옮기기

``` javascript
result.push(`<p>제목: ${person.photo.title}</p>`);
result.concat(photoData(person.photo));

function photoData(aPhoto) {
    return [
        `<p>위치: ${aPhoto.location}</p>`,
        `<p>날짜: ${aPhoto.date.toDateString()}</p>`,
    ];
}
```

=>

``` javascript
result.concat(photoData(person.photo));

function photoData(aPhoto) {
    return [
        `<p>제목: ${aphoto.title}</p>`;
        `<p>위치: ${aPhoto.location}</p>`,
        `<p>날짜: ${aPhoto.date.toDateString()}</p>`,
    ];
}
```

#### 배경

중복 제거는 코드를 건강하게 관리하는 가장 효과적인 방법 중 하나다. 호출하는 곳이 아무리 많더라도 무언가 수정할 일이 생겼을 때 한 곳만 수정하면 되도록 반복되는 부분을 피호출 함수로 합치는 방법을 사용한다.

#### 절차

- 반복 코드가 함수 호출 부분과 멀리 떨어져 있다면 문장 슬라이드하기를 적용해 근처로 옮긴다
- 타깃 함수를 호출하는 곳이 한 곳뿐이면, 단순히 소스 위치에서 해당 코드를 잘라내에 피호출 함수로 복사하고 테스트한다. 이 경우라면 나머지 단계는 무시한다.
- 호출자가 둘 이상이면 호출자 중 하나에서 '타깃 함수 호출 부분과 그 함수로 옮기려는 문장들을 함께' 다른 함수로 추출한다. 추출한 함수에 기억하기 쉬운 임시 이름을 지어준다.
- 다른 호출자 모두가 방금 추출한 함수를 사용하도록 수정한다. 하나씩 수정할 때마다 테스트한다.
- 모든 호출자가 새로운 함수를 사용하게 되면 원래 함수를 새로운 함수 안으로 인라인한 후 원래 함수를 제거한다.
- 새로운 함수의 이름을 원래 함수의 이름으로 바꿔준다(함수 이름 바꾸기)

#### 예시

사진 관련 데이터를 HTML로 내보내는 코드

### 8.4 Move Statements to Callers(문장을 호출한 곳으로 옮기기)

반대 리팩터링: 문장을 함수로 옮기기

``` javascript
emitPhotoData(outStream, person.photo);

function emitPhotoData(outStream, photo) {
    outStream.write(`<p>제목: ${aphoto.title}</p>\n`);
    outStream.write(`<p>위치: ${aPhoto.location}</p>\n`);
}
```

=> 

``` javascript
emitPhotoData(outStream, person.photo);
outStream.write(`<p>위치: ${person.photo.location}</p>\n`);

function emitPhotoData(outStream, photo) {
    outStream.write(`<p>제목: ${aphoto.title}</p>\n`);
}
```

#### 배경

초기 응집도가 높고 한 가지 일만 수행하던 함수가 어느새 둘 이상의 다른 일을 수행하게 된다.

#### 절차

- 호출자가 한두 개뿐이고 피호출 함수도 간단한 단순한 상황이면, 피호출 함수의 처음(혹은 마지막)줄(들)을 잘라내어 호출자(들)로 복사해 넣는다(필요하면 적당히 수정한다). 테스트만 통과하면 이번 리팩터링은 여기서 끝이다.
- 더 복잡한 상황에서는, 이동하지 '않길' 원하는 모든 문장을 함수로 추출한 다음 검색하기 쉬운 임시 이름을 지어준다.
- 원래 함수를 인라인한다.
- 추출된 함수의 이름을 원래 함수의 이름으로 변경한다

#### 예시

호출자가 둘 뿐인 단순한 상황

### 8.5 Replace inline Code with Function Call (인라인 코드를 함수 호출로 바꾸기)

``` javascript
let appliesToMass = false;
for(const s of states) {
    if ( s === "MA") appliesToMass = true;
}
```

=> 

``` javascript
appliesToMass = states.includes("MA");
```

#### 배경

함수의 이름이 코드의 동작 방식보다는 목적을 말해주기 때문에 함수를 활용하면 코드를 이해하기가 쉬워진다.
함수는 중복을 없애는 데도 효과적이다.

이미 존재하는 함수와 똑같은 일을 하는 인라인 코드를 발견하면 해당 코드를 함수 호출로 대체하게 되는데,
함수의 코드를 수정하더라도 인라인 코드의 동작은 바뀌지 않아야 할 때는 판단하는 데는 함수의 이름이 힌트가 된다.
이름을 잘 지었다면 인라인 코드 대신 함수 이름을 넣어도 말이 된다.

특히 라이브러리가 제공하는 함수로 대체할 수 있다면 함수 본문을 작성할 필요조차 없으므로 훨씬 좋다.

#### 절차

- 인라인 코드를 함수 호출로 대체한다.
- 테스트한다.

> 함수 추출하기와 차이점은 인라인 코드를 대체할 함수가 이미 존재하느냐의 여부.
사용중인 프로그래밍 언어의 표준 라이브러리나 플랫폼이 제공하는 API를 잘 파악하고 있을수록 이번 리팩터링의 활용 빈도가 높아진다.

### 8.6 Slide Statements (문장 슬라이드하기)

1판에서의 이름: 조건문의 공통 실행 코드 빼내기

``` javascript
const pricingPlan = retrievePricingPlan();
const order = retreiveOrder();
let charge;
const chargePerUnit = pricingPlan.unit;
```

=>

``` javascript
const pricingPlan = retrievePricingPlan();
const chargePerUnit = pricingPlan.unit;
const order = retreiveOrder();
let charge;
```

#### 배경

관련된 코드들이 가까이 모여 있다면 이해하기가 더 쉽다.
예시로 모든 변수 선언을 미리 해 두고 나중에 사용하는 방식 보다는 변수를 처음 사용할 떄 선언하는 방식으로 코드를 모은다.

#### 절차

- 코드 조각(문장들)을 이동할 목표 위치를 찾는다. 코드 조각의 원래 위치와 목표 위치 사이의 코드들을 훑어보면서, 조각을 모으고 나면 동작이 달라지는 코드가 있는지 살핀다. 다음과 같은 간섭이 있다면 이 리팩터링을 포기한다.
  - 코드 조각에서 참조하는 요소를 선언하는 문장 앞으로는 이동할 수 없다.
  - 코드 조각을 참조하는 요소의 뒤로는 이동할 수 없다.
  - 코드 조각에서 참조하는 요소를 수정하는 문장을 건너뛰어 이동할 수 없다.
  - 코드 조각이 수정하는 요소를 참조하는 요소를 건너뛰어 이동할 수 없다.
- 코드 조각을 원래 위치에서 잘라내어 목표 위치에 붙여 넣는다.
- 테스트한다.

#### 예시

무엇을 슬라이드할지와 슬라이드할 수 있는지 여부 파악.
무엇을 슬라이드할지는 맥락과 관련이 있다.
슬라이드가 실제로 가능한지 점건하려면 슬라이드할 코드 자체와 그 코드가 건너뛰어야 할 코드를 모두 살펴야 한다.

#### 예시: 조건문이 있을 때의 슬라이드

#### 더 읽을거리

문장 교환하기와의 차이
문장 교환하기는 인접한 코드 조각을 이동하지만, 문장 하나짜리 조각만 취급한다.

### 8.7 Split Loop

``` javascript
let averageAge = 0;
let totalSalary = 0;
for (const p of people) {
    averageAge += p.age;
    totalSalary += p.salary;
}
averageAge = averageAge / people.length;
```

=>

``` javascript
let totalSalary = 0;
for (const p of people) {
    totalSalary += p.salary;
}

let averageAge = 0;
for (const p of people) {
    averageAge += p.age;
}
averageAge = averageAge / people.length;
```

#### 배경

반복문 하나에 두 가지 일을 수행하는데 두 일을 한꺼번에 처리할 수 있다는 이유 때문에 그렇다.
각각의 반복문으로 분리해두면 수정할 동작 하나만 이해하면 된다.

하지만 반복문을 두 번 실행해야 하므로 불편할 수 있는데, 리팩터링과 최적화는 구분해야 한다.
최적화는 코드를 깔끔하게 정리한 이후에 수행한다.

#### 절차

- 반복문을 복제해 두 개로 만든다.
- 반복문이 중복되어 생기는 부수효과를 파악해서 제거한다.
- 테스트한다.
- 완료됐으면, 각 반복문을 함수로 추출할지 고민해본다.

#### 예시

전체 급여와 가장 어린 나이를 계산하는 코드

### 8.8 Replace Loop with Pipeline (반복문을 파이프라인으로 바꾸기)

``` javascript
const names = [];
for (const i of input) {
    if (i.job === "programmer")
        names.push(i.name);
}
```

=>

``` javascript
const names = input
    .filter(i => i.job === "programmer")
    .map(i => i.name);
```

#### 배경

Collection Pipeline을 이요하면 처리 과정을 일련의 연산으로 표현할 수 있다.
논리를 파이프라인으로 표현하면 이해하기 훨씬 쉬워진다.

#### 절차

- 반복문에서 사용하는 컬렉션을 가리키는 변수를 하나 만든다.
- 반복문의 첫 줄부터 시작해서, 각각의 단위 행위를 적절한 컬렉션 파이프라인 연산으로 대체한다. 이 때 컬렉션 파이프라인 연산은 위에서 만든 반복문 컬렉션 변수에서 시작하여, 이전 연산의 결과를 기초로 연쇄적으로 수행된다. 하나를 대체할 때마다 테스트한다.
- 반복문의 모든 동작을 대체했다면 반복문 자체를 지운다.

#### 예시

내 회사의 지점 사무실 정보를 CSV 형태로 정리한 걸 바탕으로 인도(India)에 자리한 사무실을 찾아서 도시명과 전화번호를 반환한다.

### 8.9 Remove Dead Code

``` javascript
if (false) {
    doSomethingThatUsedToMatter();
}
```

=>

``` javascript
```

#### 배경

사용되지 않는 코드가 있다면 그 소프트웨어의 동작을 이해하는 데는 커다란 걸림돌이 될 수 있다.

코드가 더 이상 사용되지 않게 됐다면 지워댜 한다. 다시 필요해질 날이 오지 않을까 걱정할 필요가 없는데 버전관리 시스템이 있기 때문이다.

#### 절차

- 죽은 코드를 외부에서 참조할 수 있는 경우라면 (예컨대 함수 하나가 통째로 죽었을 때) 혹시라도 호출하는 곳이 있는지 확인한다.
- 없다면 죽은 코드를 제거한다.
- 테스트한다.