---
description: 2024.06.07
---

# Chapter 3

#### <mark style="background-color:red;">3장. 고급 타입</mark>

**any**

JS에 존재하는 모든 값을 오류 없이 받을 수 있음.

* TS의 목적인 **정적 타이핑을 무색**하게 만들 수 있다. ( = 타입을 명시하지 않은 것과 동일)

```
💡 그럼에도 불구하고 any를 사용하는 경우
1. 개발 단계에서 임시로 값을 지정해야 할 때 (값이 변경될 가능성이 있는 경우)
2. 어떤 값을 받아올지, 넘겨줄지 정할 수 없을 때 (API 요청 및 응답처리, 콜백함수 전달 등)
3. 값을 예측할 수 없을 때 암묵적으로 사용 (Fetch API) 
```



**unknown**

any와 유사하게 모든 타입의 값이 할당될 수 있음

* unknown으로 지정한 값은 다른 변수에 할당될 수 없음
* 값을 가져오거나 내부 속성에 접근할 수 없어 엄격한 타입 검사를 강제함.
* any 보단 unknown 사용하기!



\***배민에서 any를 사용하는 경우**

* 어떤 값이 올지 모르는 상황에서 일일이 _타입 캐스팅을 해야 하는 상황_이 생길 때



**void**

1. 함수의 경우
   * JS : return type을 지정하지 않으면 default로 **undefined**으로 지정됨
   * TS : return type을 지정하지 않으면 default로 **void**으로 지정됨
2.  변수의 경우

    * void 는 undefined, null 만 할당할 수 있지만, 해당 키워드로(undefined, null) 타입을 직접 지정하는 것이 바람직함



**never** 값을 반환할 수 없는 타입

1. 에러를 던지는 경우 `throw`
2. 무한히 함수가 실행되는 경우 `while`

> 타입의 하위 타입이기 때문에 never 자기 자신을 제외한 **다른 타입에 할당될 수 없다**



**Arrary**

사전에 허용하지 않은 타입이 서로 섞이는 것을 방지하여 타입 안정성을 제공

```tsx
const array1: number[] | string[] = [1, 'abc'];
// const array1: (number | string)[] = [1, 'abc']; 
const array2: Array<number | string> = [1, 'abc'];
```

*   Tuple

    길이를 제한한 배열로 원소 개수와 타입을 보장함

**enum**

* 타입 안정성 : 명시하지 않은 다른 문자열을 인자로 받을 수 없음
* 명확한 의미 전달 및 높은 응집력
* 높은 가독성
  * 관련이 높은 멤버를 모아 문자열 상수처럼 사용하고자 할 때 유용
  * 주의 : 역방향 접근이 가능함 (`const` 로 선언하면 해결\~)
* 숫자 상수로 관리되는 enum : 선언 값 이외의 값을 할당하거나 접근할 때 이를 방지하지 못한다.
* 문자열 상수 방식으로 선언한 enum : 미리 선언하지 않은 멤버로 접근을 방지



**\[타입 조합]**

* **교차 타입 (Intersection)** 여러가지 타입을 결합하여 하나의 단일 타입으로 만드는 것

```tsx
type A = { a : string }
type B = A & { b : number }
//  두 타입 모두 만족함
```



* **유니온 타입 (Union)** A 또는 B 중 하나가 될 수 있는 타입



* **인덱스 시그니처** 특정 타입의 속성 이름은 알 수 없지만 속성 값의 타입을 알고 있을 때 사용하는 문법

```tsx
[Key: K] : T
// 해당 타입의 속성 키는 모두 K 타입이어야 하고 속성값은 모두 T 타입을 가져야 한다
```



* **인덱스드 엑세스 타입 (Indexed Access Types)** 다른 타입의 특정 속성이 가지는 타입을 조회하기 위해 사용



* **맵드 타입 (Mapped Types)** 배열 A를 기반으로 새로운 배열 B를 만들어내는 배열 메서드

`as`키워드를 사용하여 키를 재지정할 수 있다

```tsx
type BottomSheetStore = {
  [index in BOTTOM_SHEET_ID as `${index}_BOTTOM_SHEET`]: {
    resolver?: (payload: any) => void;
    args?: any;
    isOpened: boolean;
  };
};
```



* **템플릿 리터럴 타입 (Template Literal Types)** 자바스크립트의 템플릿 리터럴 문자를 사용하여 문자열 리터럴 타입을 선언할 수 있는 문법



* 제네릭 (Generic) (일반화된 데이터 타입)
  * 정적 언어에서 다양한 타입 간에 재사용성을 높이기 위해 사용하는 문법
  * 함수, 타입, 클래스 등 여러 타입에 대해 하나하나 따로 정의하지 않아도 되기 때문에 재사용성이 향상된다
  * 배열 생성 시점에 원하는 타입으로 특정함 (any와의 차이)
    * 배열 요소가 전부 동일한 타입

```tsx
const func = <T extends {}>(arg: T): T[] => {
```

`extends {}`를 사용했을 경우 원시 타입을 포함한(string, number 등) 값을 제네릭으로 받을 수 있으나, null과 undefined 는 제네릭으로 사용할 수 없다





### **Discussion Points**

1. void , undefined, never
   * `void`는 아무 것도 반환하지 않는 함수를 나타내며, 주로 부수 효과가 있는 함수에서 사용
   * `undefined`는 함수가 명시적으로 `undefined`를 반환할 때 사용
   * `never`는 함수가 정상적으로 종료되지 않음을 나타내며, 항상 예외를 던지거나 무한 루프에 빠지는 함수에서 사용

```
💡 함수의 리턴 타입은 성능에 큰 영향을 미치지 않으며,
코드의 명확성과 타입 안전성을 높이는 데 중점을 둠
```



2. enum
   *   현재 우리 프로젝트에서도 enum에 의한 에러가 종종 발생하고 있음

       ex. enum 중간에 새로운 타입을 정의
   * 그렇다면 Enum을 string으로 관리하는 것은 어떨까?