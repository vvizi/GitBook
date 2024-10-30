---
description: 2024.06.13
---

# Chapter 4

#### <mark style="background-color:red;">4장. 타입 확장하기 좁히기</mark>

**타입 확장하기** : 기존 타입을 사용해서 새로운 타입을 정의하는 것. (코드 중복을 줄일 수 있음)

`extends` `교차 타입` `유니온 타입`



* **유니온 타입**

A,B 타입 모두 MyUnion 의 타입이 된다. (A또는 B의 값 중 하나만)

```tsx
type MyUnion = A | B;
```



* **교차 타입** 기존 타입을 합쳐 하나의 타입을 만드는 것 (A또는 B의 값 모두)

```tsx
type MyUnion = A & B;
```

```
💡 type 은 교차 타입으로 선언되었을 때,
새롭게 추가되는 속성에 대해 미리 알 수 없기 때문에 선언 시 에러가 나지 않는다.
(같은 속성에 대해 서로 호환되지 않는 타입 선언 -> never로 형변환 됨)
```

> 주어진 타입에 무분별하게 속성을 추가하여 사용하는 것보다 **타입을 확장해서 사용하는 것**이 좋다.



**타입 좁히기** : 타입 가드

변수 또는 표현식의 범위를 더 작은 범위로 좁혀나가는 과정

`typeof` `instanceof` `in`

* typeof : 원시타입을 추론할 때
* instanceof : 인스턴스화된 객체 타입을 판별할 때
* in : 객체 속성 유무를 판단할 때
* is : 사용자 정의 타입 가드

```
💡 자료형 확인을 조건 분기에 사용하지 않기 (내 코드가 그렇게 이상한가요? 6장)
instanceof 지양하기

a instanceof B

구체적인 클래스나 생성자 함수에 의존하게 되며 추상화 및 캡슐화 위반한다.
a가 하위 계층인 B인 경우를 직접적으로 알 필요도 없고, 알아서는 안 된다.
조건분기 중복되는 문제 초래 리스코프 치환 원칙 위반
- 자식 객체가 부모 객체를 완전히 대체할 수 있다는 원칙
```



* 모델 타입을 판별할 때, `instanceof` 를 사용하는 case가 많음

```tsx
selectedModel instanceof NewWidgetModel
```

* 대체하기

```typescript
// NewWidgetUtil
export function isNewWidgetModel(model: unknown): model is NewWidgetModel {
    return (model as NewWidgetModel).isNewWidgetModelType() === 'newWidgetModelType';
}

// NewWidgetModel
public isNewWidgetModelType(): string {
    return 'newWidgetModelType';
}
```

