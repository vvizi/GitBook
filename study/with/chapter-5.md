---
description: 2024.06.20
---

# Chapter 5

#### <mark style="background-color:red;">5장. 타입 활용하기</mark>

> 중복되는 타입 코드를 제거하고 상황에 따라 적절한 타입을 얻을 수 있다 → `정확한 타입 추론 가능`

**조건부 타입**

`extends` `infer` `never`

```tsx
Condition ? A : B;
```

1. **extends** : 타입을 조건부로 설정할 때 활용

```tsx
T extends U ? X : Y
```

제네릭 + extends

```tsx
const useGetRegister = <T extends "card" | "appcard" | "bank">(type: T) : UseQueryResult => {
const url = `${type === "appcard" ? "card" : type}`;
```

* 제네릭으로 받는 타입을 제한하는 한정자의 역할 : 휴먼 에러 방지 가능
* 조건부 타입 사용 : 불필요한 타입 가드, 타입 단언 등을 방지



2. **infer** : extends 로 조건을 서술하고 infer로 타입을 추론하는 방식

```tsx
type UnpackPromise<T> = T extends Prominse<infer K>[] ? K : any;
// Promise<infer K> : Promise의 반환 값을 추론해 해당 값의 타입을 K라고 지정
```

* T가 promise로 래핑된 경우라면, K를 반환하고 그렇지 않으면 any를 반환



**템플릿 리터럴 타입 활용하기**

```tsx
type HeadingNumber = 1 | 2 | 3 | 4 | 5;
type HeaderTag = `h${HeadingNumber}`;
```

**`장점`**

* 읽기 쉬운 코드 작성.
* 코드를 재사용 하고 수정하는 데 용이.

**`단점`**

* ts 컴파일러가 유니온을 추론하는 데 시간이 오래 걸리면 타입을 추론하지 않고 에러를 발생시킬 수 있음.



**커스텀 유틸리티 타입 활용하기**

1. **Pick Omit**

타입 Props에서 필요한 속성 타입만 골라 사용할 수 있음.

```tsx
type StyledProps = Pick<Props, "height" | "color" | "isFull">;
```

💡

유니언 타입에서 필요한 타입만 추출 : `Extract`

유니언 타입에서 특정 타입만 제외 : `Exclude`



2. **PickOne**

ts는 서로 다른 2개 이상의 객체를 유니온 타입으로 받을 때 타입 검사가 제대로 되지 않는 이슈가 있음.

```tsx
type Card = {
card: string;
};
type Account = {
account: string;
};
function withdraw(type: Card | Account) {
/* ... */
}
withdraw({ card: "hyundai", account: "hana" });
// Card와 Account 속성을 한 번에 받아도 에러 없음
```

**해결** : 속성 중 하나만 가질 수 있도록 PickOne으로 정의

```tsx
type Card = {
  card: string;
};
type Account = {
  account: string;
};
// CardOrAccount가 Card의 속성이나 Account의 속성 중 하나만 가질 수 있게 정의
type CardOrAccount = PickOne<Card & Account>;
```

3. **NonNullable**

T가 null 또는 undefined 일 때 never 또는 T로 반환하는 타입

* null이나 undefined가 아닌 경우를 제외하기 위해 사용

```tsx
type NonNullable<T> = T extends null | undefined ? never : T;
```

**Record 원시 타입 키 개선하기** 객체 선언 시 키가 어떤 값인지 명확하지 않으면 **Record**의 키를 `string`이나 `number` 같은 원시 타입으로 명시하곤 하는데 이는 **런타임 에러**를 야기할 수 있어 주의 필요

> **1. key가 무한한 경우** → 옵셔널 체이닝(?.)을 사용 (undefined일 수 있는 값을 인지하고 코드를 작성해야 하기 때문에 예상치 못한 런타임 에러 야기) **2. 유닛 타입으로 정의** → 키가 무한해야 하는 상황에는 적합x

**해결** : Partial을 활용하여 정확한 타입 표현하기 키가 무한한 상황에서 Partial을 사용해 해당 값이 undefined일 수 있는 상태임을 표현할 수 있음

```tsx
type PartialRecord<K extends string, T > = Partial<Record<K, T>>;
type Category = string;
const foodByCategory: PartialRecord<Category, Food[]>
```

