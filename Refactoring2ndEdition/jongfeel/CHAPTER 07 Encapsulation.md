## CHAPTER 07 Encapsulation

### Discussion

특별한 논의 내용 없음

### 7.1 Encapsulate Record

1판에서는 이름: 레코드를 데이터 클래스로 전환

#### 배경

단순 레코드는 계산해서 얻을 수 있는 값과 그렇지 않은 값을 구분해야 하므로 번거로운 단점이 있다.
값의 범위를 표현하려면 '시작', '끝', '길이'를 알아야 한다.
가변 데이터를 저장하는 용도는 레코드 보다는 객체가 낫다

#### 절차

- 레코드를 담은 변수를 캡슐화 한다
- 레코드를 감싼 단순한 클래스로 해당 변수의 내용을 교체한다. 이 클래스에 원본 레코드를 반환하는 접근자도 정의하고, 변수를 캡슐화하는 함수들이 이 접근할수록 사용하도록 수정한다.
- 테스트한다 
- 원본 레코드 대신 새로 정의한 클래스 타입의 객체를 반환하는 함수들을 새로 만든다
- 레코드를 반환하는 예전 함수를 사용하는 코드를 위에서 만든 새 함수를 사용하도록 바꾼다. 필드에 접근할 때는 객체의 접근자를 사용한다. 적절한 접근자가 없다면 추가한다. 한 부분을 바꿀때마다 테스트한다.
- 클래스에서 원본 데이터를 반환하는 접근자와 원본 레코드를 반환하는 함수들을 제거한다
- 테스트한다 
- 레코드의 필드도 데이터 구조인 중첩 구조라면 레코드 캡슐화하기와 컬렉션 캡슐화하기를 재귀적으로 적용한다

#### 예시: 간단한 레코드 캡슐화하기

#### 예시: 중첩된 레코드 캡슐화하기

JSON 문서처럼 여러 겹 중첩된 레코드의 경우

### 7.2 Encapsulate Collection

``` javascript
class Person {
    get courses() { return this.courses; }
    set courses(aList) { this._courses = aList; }
}
```

=>

``` javascript
class Person {
    get courses() { return this._courses.slice(); }
    addCourse(aCourse) { ... }
    removeCourse(aCourse) { ... }
}
```

#### 배경

Collection getter가 원본 collection을 반환하지 않게 만들어서 클라이언트가 실수로 collection을 바꿀 가능성을 차단하는게 좋다.

내부 collection을 직접 수정하지 못하게 메서드를 따로 만드는 것 보다 collection pipeline pattern을 적용해서 조합하는 방식이 낫다.

다른 방식으로 읽기 전용으로 제공한다. 컬렉션 게터를 제공하고 내부 컬렉션의 복제본을 반환한다.

코드베이스에 일관성을 줘서 한 가지 방식으로 컬렉션 접근 함수의 동작 방식을 통일한다.

#### 절차

- 아직 컬렉션을 캡슐화하지 않았다면 변수 캡슐화하기부터 한다.
- 컬렉션에 원소를 추가/제거하는 함수를 추가한다.
- 정적 검사를 수행한다.
- 컬렉션을 참조하는 부분을 모두 찾는다. 컬렉션의 변경자를 호출하는 코드가 모두 앞에서 추가/제거 함수를 호출하도록 수정한다. 하나씩 수정할 때마다 테스트한다.
- 컬렉션 게터를 수정해서 원본 내용을 수정할 수 없는 읽기전용 프락시나 복제본을 반환하게 한다.
- 테스트 한다.

#### 예시

수업(course) 목록을 필드로 지니고 있는 Person 클래스의 예시

Person 클래스

``` javascript
get courses() { return this._courses.slice(); }
```

위와 같이 courses의 복제본을 리턴하는 식으로 만든다.

### 7.3 Replace Primitive with Object (기본형을 객체로 바꾸기)

1판에서의 이름

- 데이터 값을 객체로 변환
- 분류 부호를 클래스로 변환

``` javascript
orders.filter(o => "high" === o.priority || "rush" === o.priority);
```

=> 

``` javascript
orders.filter(o => o.priority.higherThan(new Prioirty("norma;")));
```

#### 배경

개발 초기에 단순한 정보를 숫자나 문자열 같은 간단한 데이터 항목으로 표현.
개발이 진행되면 전화번호에서 지역보다 추출이나 포맷팅 같은 로직이 추가되고 중복 코드가 늘어나서 사용할 때 마다 드는 노력도 증가한다.

출력 기능 이상이 필요해 지면 데이터를 표현하는 전용 클래스를 만든다.
나중에 특별한 동작이 필요해지면 이 클래스에 추가한다.

#### 절차

- 아직 변수를 캡슐화하지 않았다면 캡슐화한다.
- 단순한 값 클래스를 만든다. 생성자는 기본 값을 인수로 받아서 저장하고, 이 값을 반환하는 게터를 추가한다.
- 정적 검사를 수행한다.
- 값 클래스의 인스턴스를 새로 만들어서 필드에 저장하도록 세터를 수정한다. 이미 있다면 필드의 타입을 적절히 변경한다.
- 새로 만든 클래스의 게터를 호출한 결과를 반환하도록 게터를 수정한다.
- 테스트한다.
- 함수 이름을 바꾸면 원본 접근자의 동작을 더 잘 드러낼 수 있는지 검토한다.

#### 예시

레코드 구조에서 데이터를 읽어 들이는 단순한 주문(order) 클래스

### 7.4 Replace Temp with Query (임시 변수를 질의 함수로 바꾸기)

``` javascript
const basePrice = this._quantity * this._itemPrice;
if (basePrice > 1000)
    return basePrice * 0.95;
else
    return basePrice * 0.98;
```

=>

``` javascript
get basePrice() = { this._quantity * this._itemPrice; }
if (this.basePrice > 1000)
    return this.basePrice * 0.95;
else
    return this.basePrice * 0.98;
```

#### 배경

임시 변수를 사용해서 값을 계산하는 코드가 반복되는걸 줄이고 값의 의미를 설명할 수 있어 유용하지만 함수로 만드는게 나을 수 있다.

변수 대신 함수로 만들어 두면 비슷한 계산을 수행하는 다른 함수에서도 사용할 수 있어 코드 중복이 줄어든다.

이번 리팩터링은 클래스 내에서 적용할 때 효과가 가장 크다.

#### 절차

- 변수가 사용되기 전에 값이 확실히 결정되는지, 변수를 사용할 때마다 계산 로직이 매번 다른 결과를 내지는 않는지 확인한다.
- 읽기전용으로 만들 수 있는 변수는 읽기전용으로 만든다
- 테스트한다.
- 변수 대입문을 함수로 추출한다.
- 테스트한다.
- 변수 인라인하기로 임시 변수를 제거한다.

#### 예시

간단한 주문(order) 클래스

### 7.5 Extract Class

반대 리팩터링: 클래스 인라인하기

``` javascript
class person {
    get officeAreaCode() { return this._officeAreaCode; }
    get officeNumber() { return this._officeNumber; }
}
```

=>

``` javascript
class Person {
    get officeAreaCode() { return this._telephoneNumber.areaCode; }
    get officeNumber() { return this._telephoneNumber.number; }
}
class TelephoneNumber {
    get areaCode() { return this._areaCode; }
    get number() { return this._number; }
}
```

#### 배경

클래스에 몇 가지 연산을 추가하고 데이터도 보강하면서 클래스가 점점 비대해진다.

데이터와 메서드를 따로 묶을 수 있다면 분리하자는 신호이다. 함께 변경되는 일이 많거나 서로 의존하는 데이터들도 분리한다. 제거해도 다른 필드나 메서드들이 논리적으로 문제가 없다면 분리할 수 있다는 뜻이다.

확장해야 할 기능이 무엇이내에 따라 서브클래스를 만드는 방식도 달라진다면 클래스를 나눠야 하는 신호다.

#### 절차

- 클래스의 역할을 분리할 방법을 정한다.
- 분리될 역할을 담당할 클래스를 새로 만든다.
- 원래 클래스의 생성자에서 새로운 클래스의 인스턴스를 생성하여 필드에 저장해둔다.
- 분리될 역할에 필요한 필드들을 새 클래스로 옮긴다(필드 옮기기), 하나씩 옮길때마다 테스트한다.
- 메서드들도 새 클래스로 옮긴다(함수 옮기기), 이때 저수준 메서드, 즉 다른 메서드를 호출하기보다는 호출을 당하는 일이 많은 메서드부터 옮긴다. 하나씩 옮길 때마다 테스트한다.
- 양쪽 클래스의 인터페이스를 살펴보면서 불필요한 메서드를 제거하고, 이름도 새로운 환경에 맞게 바꾼다.
- 새 클래스를 외부로 노출할지 정한다. 노출하려거든 새 클래스에 참조를 값으로 바꾸기를 적용할지 고민해본다.

#### 예시

단순한 Person 클래스의 예시

### 7.6 Inline Class

반대 리팩터링: 클래수 추출하기

``` javascript
class Person {
    get officeAreaCode() { return this._telephoneNumber.areaCode; }
    get officeNumber() { return this._telephoneNumber.number; }
}
class TelephoneNumber {
    get areaCode() { return this._areaCode; }
    get number() { return this._number; }
}
```

=>

``` javascript
class person {
    get officeAreaCode() { return this._officeAreaCode; }
    get officeNumber() { return this._officeNumber; }
}
```

#### 배경

클래스 추출하기를 거꾸로 돌리는 리팩터링.
제 역할을 못하는 클래스는 인라인한다.

두 클래스의 기능을 지금과 다르게 배분하고 싶을 때도 클래스를 인라인한다.

#### 절차

- 소스 클래스의 각 public 메서드에 대응하는 메서드들을 타깃 클래스에 생성한다. 이 메서드들은 단순히 작업을 소스 클래스로 위임해야 한다.
- 소스 클래스의 메서드를 사용하는 코드를 모두 타깃 클래스의 위임 메서드를 사용하도록 바꾼다. 하나씩 바꿀 때마다 테스트한다.
- 소스 클래스의 메서드와 필드를 모두 타깃 클래스로 옮긴다. 하나씩 옮길 때마다 테스트한다.
- 소스 클래스를 삭제하고 조의를 표한다.

#### 예시

배송 추저 정보를 표현하는 TrackingInformation 클래스

### 7.7 Hide Delegate

반대 리팩터링: 중개자 제거하기

``` javascript
manager = aPerson.department.manager;
```

=>

``` javascript
manager = aPerson.manager;

class Person {
    get manager() { return this.department.manager; }
}
```

#### 배경

모듈화 설계를 제대로 하는 핵심은 캡슐화다. 캡슐화는 모듈들이 시스템의 다른 부분에 대해 알아야만 내용을 줄여준다. 캡슐화가 잘 되어 있다면 무언가를 변경해야 할 때 함께 고려해야 할 모듈 수가 적어져서 코드를 변경하기가 훨씬 쉬워진다.

#### 절차

- 위임 객체의 각 메서드에 해당하는 위임 메서드를 서버에 생성한다.
- 클라이언트가 위임 객체 대신 서버를 호출하도록 수정한다. 하나씩 바꿀 때마다 테스트한다.
- 모두 수정했다면, 서버로부터 위임 객체를 얻는 접근자를 제거한다.
- 테스트한다.

#### 예시

사람(person)과 사람이 속한 부서(department)를 정의

### 7.8 Remove Middle Man (중개자 제거하기)

반대 리팩터링: 위임 숨기기

``` javascript
manager = aPerson.manager;

class Person {
    get manager() { return this.department.manager; }
}
```

=>

``` javascript
manager = aPerson.department.manager;
```

#### 배경

단순히 전달만 하는 위임 메서드들이 점점 성가셔지면, 서버 클래스는 중개자 역할로 전락하게 되고 차라리 클라이언트가 위임 객체를 직접 호출하는게 나을 수 있다.

> 이 냄새는 테메테르 법칙(Law of Demeter)을 너무 신봉할 때 자주 나타난다. '이따금 유용한 데메테르의 제안' 정도로 부르는게 낫다

시스템이 바뀌면 '적절하다'의 기준도 바뀌므로 캡슐화가 어색해지면 즉시 고친다.

#### 절차

- 위임 객체를 얻는 게터를 만든다.
- 위임 메서드를 호출하는 클라이언트가 모두 이 게터를 거치도록 수정한다. 하나씩 바꿀 때마다 테스트한다.
- 모두 수정했다면 위임 메서드를 삭제한다.

#### 예시

자신이 속한 부서(department) 객체를 통해 관리자(manager)를 찾는 사람(person) 클래스

### 7.9 Substitute Algorithm (알고리즘 교체하기)

``` javascript
function foundPerson(people) {
    for (let i=0; i < people.length; i++) {
        if (people[i] === "Don") {
            return "Don";
        }
        if (people[i] === "John") {
            return "John";
        }
        if (people[i] === "Kent") {
            return "Kent";
        }
    }
    return "";
}
```

=>

``` javascript
function foundPerson(people) {
    const candidates = [ "Don", "John", "Kent" ];
    return people.find(p => candidates.includes(p)) || '';
}
```

#### 배경

문제를 더 확실히 이해하고 훨씬 쉽게 해결하는 방법을 발견했을 때 기존 알고리즘 전체를 걷어내고 훨씬 간결한 알고리즘으로 바꾼다.

이 작업에 착수하시면 반드시 메서드를 가능한 한 잘게 나눴는지 확인해야 한다.

#### 절차

- 교체할 코드를 함수 하나에 모은다.
- 이 함수만을 이용해 동작을 검증하는 테스트를 마련한다.
- 대체할 알고리즘을 준비한다.
- 정적 검사를 수행한다.
- 기존 알고리즘과 새 알고리즘의 결과를 비교하는 테스트를 수행하낟. 두 결과가 같다면 리팩터링이 끝난다. 그렇지 않다면 기존 알고리즘을 참고해서 새 알고리즘을 테스트하고 디버깅한다.