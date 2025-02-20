---
description: 2024.05.24
---

# Chapter 2

#### <mark style="background-color:red;">2장. 타입</mark>

> _타입 시스&#xD15C;_&#xC740; 코드에서 사용되는 유효한 값의 범위를 제한해서 런타임에서 발생할 수 있는 유효하지 않은 값에 대한 에러를 방지해준다.

**타입 결정 시점**

* 정적 타입 시스템 : 컴파일 시점 (기계<컴퓨터, 엔진>가 소스코드를 이해할 수 있도록 기계어로 변환되는 시점)
  * c, java, ts (직접 타입을 정의할 필요 o)
    * 참고. ts를 컴파일 하면 타입이 제거된 js 소스코드만 남게됨.
* 동적 타입 시스템 : 런타임 시점 (변환된 파일이 메모리에 적재되어 실행되는 시점)
  * python, js (직접 타입을 정의할 필요 x)

**Type Annotation**

변수, 상수, 함수의 인자와 반환 값에 타입을 명시적으로 선언해서 어떤 타입 값이 저장될 것인지 컴파일러에게 직접 알려주는 문법



**구조적 타이핑 (Structural type system)**

이름으로 타입을 구분하지 않고 구조적으로 타입을 구분한다.

```tsx
interface A {
num : number
}

interface B {
num: number
}

let a: A = {num :1}
let b: B = {num: 2}

a = b (ok)
b = a (ok)
```



**구조적 서브 타이핑 (structural subtyping)**

특정 값이 여러 타입을 동시에 가질 수 있다.

```tsx
string | number
```



**점진적 타입 확인 (gradually typed)**

컴파일 타임에 타입을 검사하면서 필요에 따라 타입 선언 생략을 허용하는 방식



**배민에서 enum vs union type**

* `enum` : 값이기 때문에 iterable하다
* `union type` : 어떤 타입을 가지고 있는지 전부 기억해야 하고, 변경이 필요한 부분은 모두 찾아서 바꿔줘야 한다. 타입이어서 순회가 안된다.



**원시타입**

1.  **boolean** 원시 값은 아니지만, 형 변환을 통해 `true / false` 로 취급되는 Truthy / Falsy 값이 있다.

    > Falsy 값 : `false`,`0`, `""(빈 문자열)`, `null`, `undefined`, `NaN`
2.  **undefined** 값이 존재하지 않음 / 할당되지 않은 값

    > typeof undefined : `undefined`
3.  **null** 알 수 없는 값

    > typeof null : `object` -> **객체라는 의미X** 언어상의 오류
    >
    > null은 별도의 고유한 자료형을 가지는 특수 값으로 객체가 아님
    >
    > JS 하위 호환성을 유지하기 위해 오류를 남겨둠
4. **number** `NaN`, `Infinity` 포함
5. **bigInt** `number` 타입과 상호작용 불가능
6. **string**
7. **symbol** `symbol()` 함수를 사용하면 어떤 값과도 _중복되지 않는 유일한 &#xAC12;_&#xC744; 생성할 수 있다



**객체 타입**

1. **object** `object` 타입은 `any` 타입과 유사하게 객체에 해당하는 모든 타입 값을 유동적으로 할당할 수 있어 지양한다
2. **{}** 객체 리터럴 방식으로 객체를 생성할 때 사용. 빈 객체 선언 시, 유틸리티 타입으로 `Record<string, never>` 사용을 지향한다.
3. **array** 하나의 타입 값만 가질 수 있음
4.  **type과 interface** 객체를 타이핑 하기 위해 사용

    > ts에서 변수 타입을 명시적으로 선언하지 않아도 컴파일러가 자동으로 타입을 추론한다.&#x20;
    >
    > 모든 변수에 일일이 명시적으로 선언할 필요는 없음 -> 개발 편의를 위해 필요할 순 있음 (컨벤션)


5.  **배민에서 type vs interface**

    **type** : 좁은 범위 / 정적인 값 사용 시 / 유니온 및 교차타입 사용 시

    **interface** : global 범위 / 확장될 수 있는 값 / 객체지향 상속
6.  **function** `function` 키워드 자체를 타입으로 사용하지는 않음

    > 함수 자체의 타입을 명시할 때는 화살표 함수 방식으로 호출 시그니처를 정의할 수 있다 함수의 타입 안정성을 보장하고, 코드의 명확성을 높일 수 있음
