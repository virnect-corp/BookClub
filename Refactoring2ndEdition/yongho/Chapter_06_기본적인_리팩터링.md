# 6.1 함수 추출하기

## 배경

- 길이를 기준으로 삼을 수 있다.
- 재사용성을 기준으로 할 수 있다.
- 두 번 이상 사용될 코드는 함수로 만든다.
- 코드를 보고 무슨 일을 하는지 파악하는 데 한참이 걸린다면 그 부분을 함수로 추출한 뒤 `무슨 일`에 걸맞은 이름을 짓는다.
- 함수는 아주 짧게
- 함수 이름을 잘 지어야 한다.

## 절차

1. 함수를 새로 만들고 목적을 잘 드러내는 이름을 붙인다. (`어떻게`가 아닌 `무엇을` 하는지가 드러나야 한다.
2. 추출할 코드를 원본 함수에서 복사하여 새 함수에 붙여 넣는다.
3. 추출한 코드 중 원본 함수의 지역 변수를 참조하거나 추출한 함수의 유효범위를 벗어나는 변수는 없는지 검사한다. 있다면 매개변수로 전달한다.
4. 변수를 다 처리했다면 컴파일한다.
5. 원본 함수에서 추출한 코드 부분을 새로 만든 함수를 호출하는 문장으로 바꾼다. (즉, 추출한 함수로 일을 위힘한다.
6. 테스트한다.
7. 다른 코드에 방금 추출한 것과 똑같거나 비슷한 코드가 없는지 살핀다. 있다면 방금 추출한 새 함수를 호출하도록 바꿀지 검토한다. (인라인 코드를 함수 호출로 바꾸기)

# 6.2 함수 인라인하기

```jsx
function getRating(driver) {
	return moreThanFiveLateDeliveries(driver) ? 2 : 1;
}

function moreThanFiveLateDeliveries(driver){
	return driver.number0fLateDeliveries › 5;
}
```

```jsx
function getRating(driver){
	return (driver.numberOfLateDeliveries > 5) ? 2 : 1;
}
```

## 배경

- 함수 본문이 이름만큼 명확한 경우 다시 인라인 한다.

## 절차

1. 다형 메서드인지 확인한다.
→ 서브클래스에서 오버라이드하는 메서드는 인라인하면 안된다.
2. 인라인할 함수를 호출하는 곳을 모두 찾는다.
3. 각 호출문을 함수 본문으로 교체한다.
4. 하나씩 교체할 때마다 테스트한다.
→ 인라인 작업을 한 번에 처리할 필요는 없다. 
인라인하기가 까다로운 부분이 있다면 일단 남겨두고 여유가 생길 때마다 틈틈이 처리한다.
5. 함수 정의(원래 함수)를 삭제한다.

# 6.3 변수 추출하기

반대 리팩터링: 변수 인라인하기 6.4절

```jsx
return order.quantity * order.itemPrice -
	Math.max(0, order.quantity - 500) * order.itemPrice * 0.05 +
	Math.min(order.quantity * order.itemPrice * 0.1, 100) ;
```

```jsx
const basePrice = order.quantity * order.itemPrice;
const quantityDiscount = Math.max(0, order.quantity - 500)
	* order.itemPrice * 0.05;
const shipping = Math.min(basePrice * 0.1, 100);
return basePrice - quantityDiscount + shipping;
```

## 배경

- 표현식이 너무 복잡해서 이해하기 어려울 때 사용
- 지역 변수를 활용해 표현식을 쪼개서 관리하여 더 쉽게 표현
- 복잡한 로직을 구성하는 단계마다 이름을 붙일 수 있어서 코드의 목적을 훨씬 명확하게 드러낼 수 있다.
- 현재 함수 안에서만 의미가 있다면 변수로 추출
- 더 넓은 범위에서 의미가 있다면 함수로 추출

## 절차

1. 추출하려는 표현식에 부작용은 없는지 확인한다. 
2. 불변 변수를 하나 선언하고 이름을 붙일 표현식의 복제본을 대입한다. 
3. 원본 표현식을 새로 만든 변수로 교체한다.
4. 테스트한다.
5. 표현식을 여러 곳에서 사용한다면 각각을 새로 만든 변수로 교체한다. 하나 교체할 때마다 테스트한다.

# 6.4 변수 인라인하기

```jsx
let basePrice = anOrder.basePrice;
return (basePrice › 1000);
```

```jsx
return anOrder.basePrice>1000;
```

## 배경

- 변수 이름이 원래 표현식과 다를 바 없을 때 사용
- 변수를 인라인

## 절차

1. 대입문의 우변(표현식)에서 부작용이 생기지는 않는지 확인한다.
2. 변수가 `const`로 선언되지 않았다면 불변으로 만든 후 테스트한다. 
→ 변수에 값이 단 한 번만 대입되는지 확인할 수 있다.
3. 이 변수를 가장 처음 사용하는 코드를 찾아서 대입문 우변의 코드로 바꾼다. 
4. 테스트한다. 
5. 변수를 사용하는 부분을 모두 교체할 때까지 이 과정을 반복한다. 
6. 변수 선언문과 대입문을 지운다.
7. 테스트한다.

# 6.5 함수 선언 바꾸기

```jsx
function circum (radius) {...}
```

```jsx
function circumference (radius) {...}
```

## 배경

- 가장 중요한 요소는 함수의 이름이다.
- 이름이 좋으면 구현 코드를 살펴볼 필요 없이 호출문만 보고도 무슨 일을 하는지 파악
- 더 나은 이름이 떠오르는 즉시 바꿔라.

## 절차

### 간단한 절차

1. 매개변수를 제거하려거든 먼저 함수 본문에서 제거 대상 매개변수를 참조하는 곳이 없는지 확인한다.
2. 매서드 선언을 원하는 형태로 바꾼다.
3. 기존 메서드 선언을 참조하는 부분을 모두 찾아서 바뀐 형태로 수정한다. 
4. 테스트한다.

### 마이그레이션 절차

1. 이어지는 추출 단계를 수월하게 만들어야 한다면 함수의 본문을 적절히 리팩터링한다.
2. 함수 본문을 [새로운 함수로 추출](https://www.notion.so/Chapter-06-df2fdebb63b448a9a32df0c0dfe392fe)한다.
3. 추출한 함수에 매개변수를 추가해야 한다면 `간단한 절차`를 따라 추가한다.
4. 테스트한다.
5. 기존 [함수를 인라인](https://www.notion.so/Chapter-06-df2fdebb63b448a9a32df0c0dfe392fe)한다.
6. 이름을 임시로 붙여뒀다면 함수 선언 바꾸기를 한 번 더 적용해서 원래 이름으로 되돌린다.
7. 테스트한다.

# 6.6 변수 캡슐화하기

```jsx
let defaultOwner = { firstName: "마틴", lastName: "파울러" };
```

```jsx
let defaultOwnerData = { firstName: "마틴", lastName: "파울러" };
export function defaultOwner() { return defaultOwnerData; }
export function setDefaultOwner (arg) { defaultOwnerData = arg; }
```

## 배경

- 접근할 수 있는 범위가 넓은 데이터를 옮길 때는 먼저 그 데이터로의 접근을 독점하는 함수를 만드는 식으로 캡슐화 하는 것이 가장 좋은 방법일 때가 많다.
- 데이터 재구성이라는 어려운 작업을 함수 재구성이라는 더 단순한 작업으로 변환하는 것이다.

## 절차

1. 변수로의 접근과 갱신을 전담하는 캡슐화 함수들을 만든다.
2. 정적 검사를 추가한다.
3. 변수를 직접 참조하던 부분을 모두 적절한 캡슐화 함수로 호출로 바꾼다. 하나씩 바꿀 때마다 테스트한다.
4. 변수의 접근 범위를 제한한다.
→ 변수로의 직접 접근을 막을 수 없을 때도 있다. 
그럴 때는 변수 이름을 바꿔서 테스트해보면 해당 변수를 참조하는 곳을 쉽게 찾아낼 수 있다.
5. 테스트한다.
6. 변수 값이 레코드라면 레코드 캡슐화하기를 적용할지 고려해본다.

# 6.7 변수 이름 바꾸기

```jsx
let a = height * width; 
```

```jsx
let area = height * width;
```

## 배경

- 변수는 프로그래머가 하려는 일에 관해 많은 것을 설명해준다.
- 함수 호출 한 번으로 끝나지 않고 값이 영속되는 필드라면 이름에 더 신경 써야 한다.

## 절차

1. 폭넓게 쓰이는 변수라면 변수 캡슐화하기를 고려한다.
2. 이름을 바꿀 변수를 참조하는 곳을 모두 찾아서, 하나씩 변경한다.
→ 다른 코드베이스에서 참조하는 변수는 외부에 공개된 변수이므로 이 리팩터링을 적용할 수 없다.
→ 변수 값이 변하지 않는다면 다른 이름으로 복제본을 만들어서 하나씩 점진적으로 변경한다.
하나씩 바꿀 때마다 테스트한다. 
3. 테스트한다. 

# 6.8 매개변수 객체 만들기

```jsx
function amountInvoiced (startDate, endDate) {...}
function amountReceived (startDate, endDate) {...}
function amountOverdue (startDate, endDate) {...}
```

```jsx
function amountInvoiced (aDateRange) {...}
function amountReceived (aDateRange) {...}
function amountOverdue (aDateRange) {...}
```

## 배경

- 데이터 항목 여러 개가 이 함수에서 저 함수로 함께 몰려다니는 경우 데이터 구조를 하나로 모아준다.
- 데이터 사이의 관계가 명확해진다.
- 매개변수 수가 줄어든다.
- 항상 똑같은 이름을 사용하기 때문에 일관성도 높아진다.

## 절차

1. 적당한 데이터 구조가 아직 마련되어 있지 않다면 새로 만든다.
→ 개인적으로 클래스로 만드는 걸 선호한다. 나중에 동작까지 함께 묶기 좋기 때문이다. 나는 주로 데이터 구조를 값 객체로 만든다.
2. 테스트한다.
3. 함수 선언 바꾸기로 새 데이터 구조를 매개변수로 추가한다. 
4. 테스트한다.
5. 함수 호출 시 새로운 데이터 구조 인스턴스를 넘기도록 수정한다. 하나씩 수정할 때마다 테스트한다. 
6. 기존 매개변수를 사용하던 코드를 새 데이터 구조의 원소를 사용하도록 바꾼다.
7. 다 바꿨다면 기존 매개변수를 제거하고 테스트한다.

# 6.9 여러 함수를 클래스로 묶기

```jsx
function base (aReading) {...}
function taxableCharge (aReading) {...}
function calculateBaseCharge(aReading){...}
```

```jsx
class Reading {
	base() {...}
	taxableCharge() {...}
	calculateBaseCharge() {...}
}
```

## 배경

- 클래스는 객체 지향 언어의 기본인 동시에 다른 패러다임 언어에도 유용하다.
- 클래스로 묶으면 이 함수들이 공유하는 공통 환경을 더 명확하게 표현할 수 있다.

## 절차

1. 함수들이 공유하는 공통 데이터 레코드를 캡슐화 한다. 
→ 공통 데이터가 레코드 구조로 묶여 있지 않다면 먼저 매개변수 객체 만들기로 데이터를 하나로 묶는 레코드를 만든다.
2. 공통 레코드를 사용하는 함수 각각을 새 클래스로 옮긴다. (함수 옮기기 8.1절)
→ 공통 레코드의 멤버는 함수 호출문의 인수 목록에서 제거한다. 
3. 데이터를 조작하는 로직들은 함수로 추출 (6.1절)해서 새 클래스로 옮긴다. 

# 6.10 여러 함수를 변환 함수로 묶기

```jsx
function base (aReading) (...}
function taxableCharge (aReading) {...}
```

```jsx
function enrichReading(argReading){
	const aReading =_.cloneDeep(argReading);
	aReading.baseCharge = base (aReading);
	aReading.taxableCharge = taxableCharge(aReading);
	return aReading;
}
```

## 배경

- 정보가 사용되는 곳마다 같은 도출 로직이 반복되기도 한다.
- 원본 데이터가 코드 안에서 갱신될 때는 클래스로 묶는 편이 훨씬 낫다.
- 여러 함수를 한데 묶는 이유 하나는 도출 로직이 중복되는 것을 피하기 위해서다.

## 절차

1. 변환할 레코드를 입력받아서 값을 그대로 반환하는 변환 함수를 만든다.
→ 이 작업은 대체로 깊은 복사로 처리해야 한다. 변환 함수가 원본 레코드를 바꾸지 않는지 검사하는 테스트를 마련해두면 도움 될 때가 많다.
2. 묶을 함수 중 함수 하나를 골라서 본문 코드를 변환 함수로 옮기고, 처리 결과를 레코드에 새 필드로 기록한다. 그런 다음에 클라이언트 코드가 이 필드를 사용하도록 수정한다. 
→ 로직이 복잡하면 함수 추출하기(6.1절)부터 한다. 
3. 테스트한다. 
4. 나머지 관련 함수도 위 과정에 따라 처리한다.

# 6.11 단계 쪼개기

```jsx
// 단계 쪼개기 전
const orderData = orderString.split(/\s+/);
const productPrice = priceList[orderData[0].split(" ")[1]];
const orderPrice = parseInt (orderData[1]) * productPrice;
```

```jsx
// 단계 쪼개기 후
const orderRecord = parseOrder (order);
const orderPrice = price (orderRecord, priceList);
function parseOrder (aString) {
	const values = aString.split(/\s+/);
	return ({
		productID: values[0].split("-")[1],
		quantity: parseInt(values[1]),
	});
}
function price(order, priceList) {
 return order.quantity * priceList[order.productID];
}
```

## 배경

- 서로 다른 두 대상을 한꺼번에 다루는 코드를 발견하면 각각을 별개의 모듈로 나누는 방법을 모색
- 코드를 수정해야 할 때 두 대상을 동시에 생각할 필요 없이 하나에만 집중
- 코드 영역들을 별도 모듈로 분리하면 그 차이를 코드에서 훨씬 분명하게 드러낼 수 있다.

## 절차

1. 두 번째 단계에 해당하는 코드를 독립 함수로 추출한다.
2. 테스트한다.
3. 중간 데이터 구조를 만들어서 앞에서 추출한 함수의 인수로 추가한다.
4. 테스트한다.
5. 추출한 두 번째 단계 함수의 매개변수를 하나씩 검토한다. 그 중 첫 번째 단계에서 사용되는 것은 중간 데이터 구조로 옮긴다. 하나씩 옮길 때마다 테스트한다.
→ 간혹 두번째 단계에서 사용하면 안 되는 매개변수가 있다. 이럴 때는 각 매개변수를 사용한 결과를 중간 데이터 구조의 필드로 추출하고, 이 필드의 값을 설정하는 문장을 호출한 곳으로 옮긴다.
6. 첫 번째 단계 코드를 함수로 추출하면서 중간 데이터 구조를 반환하도록 만든다.
→ 이때 첫 번째 단계를 변환기 객체로 추출해도 좋다.