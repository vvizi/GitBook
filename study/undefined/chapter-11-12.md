---
description: 2024.03.22
---

# Chapter 11 \~ 12

### **Summary**

#### <mark style="background-color:red;">11장. 유지 보수와 변경의 정확성을 높이는 주석 작성 방법</mark>

`요약 : 주석을 잘 적으면 코드 이해를 돕고, 대충 적으면 버그의 원인이 된다`

주석을 유지보수 하는 것은 어렵기 때문에, 실제 코드와 내용이 다른 경우가 많다

**주석을 잘 다는 방법**

1. 의도를 제대로 담아 주석을 달기
2. 로직의 동작을 설명하는 주석은 지양하기

* 메서드의 이름을 제대로 짓는다면 주석이 필요 없을 수 있다.
* 주석 때문에 이름을 대충 짓는 경우가 생길 수 있음
  * 의미 전달이 중요하다고 생각함

#### <mark style="background-color:red;">12장. 메서드(함수) : 좋은 클래스에는 좋은 메서드가 있다</mark>

`요약 : 메서드 설계 ∝ 클래스 설계`

**getter/setter 의 문제점**

* 다른 클래스를 확인하고 조작하는 메서드 구조가 되기 쉽다
*   여러 컨트롤러에서 의존하고 있는 설계에서 병행처리를 수행한다면, 문제가 발생할 수 있다

    → 개발 생산성이 좋지 않은 코드에서 발견됨
*   캡슐화가 아님

    → 데이터를 조작하는 로직을 하나의 클래스로 만들고, 필요한 메서드만 외부에 공개해야 한다.
* 상태 변경과 추출을 동시에 하는 메서드는 여러 문제의 원인이 된다.

**해결**

* 커맨드-쿼리 분리 패턴 : 메서드는 커맨드 또는 쿼리 중에 하나만 설계하도록 한다는 패턴
  * 커맨드 : 상태를 변경하는 것
  * 쿼리 : 상태를 리턴하는 것
  * 모디파이어 : 커맨드와 쿼리를 동시에 하는 것

**매개 변수 사용시 주의할 점**

1. 불변 매개변수로 만들기 : 새로운 변수에 재할당 하기
2. 플래그 매개변수 사용하지 않기
3. `null` 전달하지 않기
4. `return` 값에 매개변수 사용하지 않기
5. 매개변수는 최대한 적게 사용하기

**리턴값 사용 시 주의할 점**

1. 자료형을 사용해서 리턴 값의 의도 나타내기 (기본 자료형 x)
2. `null` 리턴하지 않기
3. 오류는 리턴 값으로 리턴하지 않고 예외 발생 시키기

생각해볼 점.

* `return undefined` 말고 `try catch` 쓰라고 하는 건가?



### **Discussion Points**

Q. 리턴 값 사용 시 주의할 점에 대한 궁금증 (오류는 리턴 값으로 리턴 하지 않고 예외 발생시키기)

* 컬렉션에서 특정 요소를 찾는 함수에 특정 요소가 없을 때 (DB에서 값을 가져올 때 X) 보통 `return undefined`로 처리해왔는데, 이럴 때는 어떻게 처리하는 게 **best** 인가요?!

A1. **Undefined 반환** : 호출하는 측에서 `undefined`를 체크하는 추가 로직이 필요하다.

* `default` 값을 반환할 수도 있음

A2. **예외 발생** : 요소가 반드시 존재해야 한다면, 예외를 발생시키는 것이 명확한 처리일 수 있다. (`try catch` )

\-> **필수 요소라면 예외를 던져 호출 측에 명확하게 알리고, 선택적 요소라면** `undefined`**를 반환하는 방식**



### **Apply**

매개변수와 리턴 값의 명확한 사용

* **불변 매개변수**로 값을 재할당하지 않으며, 매개변수로 전달한 값을 **직접 변경하지 않도록** 한다.
* 기본 자료형 대신 **명확한 타입**을 사용하고 `null` 대신 명확한 반환 값(`undefined`) 또는 **에러 처리**를 한다.

```typescript
// Before
const fetchAppList = async (
    appStore: AppStore,
    appId: number
) => {
    await appStore.downloadAppList();
    appStore.setAppList(await appStore.fetchAppList(appId));
};

// After
const fetchAppList = async (
    appStore: AppStore,
    appId: number
): Promise<void> => {
    try {
        await appStore.downloadAppList();
        const appList = await appStore.fetchAppList(appId);
        appStore.setAppList(appList);
    } catch (e) {
        dError(e);
    }
};
```



### Retrospective

리턴 값 대신 예외로 오류를 처리하는 방식이 코드의 신뢰성을 높일 수 있다.

* 리턴 값으로 오류를 처리하면 호출 측에서 해당 값을 항상 검사해야 하기 때문
