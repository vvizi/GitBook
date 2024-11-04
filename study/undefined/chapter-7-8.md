---
description: 2024.02.29
---

# Chapter 7 \~ 8

### **Summary**

#### <mark style="background-color:red;">7장. 컬렉션: 중첩을 제거하는 구조화 테크닉</mark>

`요약 : 중첩은 피할 수 있으면 피하자~`

**\[중첩 피하기]**

* 반복문 안에 조건문이 있는 경우 표준 라이브러리 제공 메서드로 변경 권장함.
  * `map(), find(), some(), every()` 등

```
map() : 배열 내의 모든 요소에 대하여 함수 결과를 모아 새로운 배열을 반환
find() : 배열에서 함수를 만족하는 첫 번째 요소를 반환
some() : 배열 안의 요소가 함수를 만족하면 true 반환 (반대 false 반환)
every() : 배열의 모든 요소가 함수를 통과하는지 테스트
```

* 조기 continue, 조기 break 로 중첩 제거하기
  * 중첩 if 대신 continue, break 사용

**\[응집도가 낮은 컬렉션 처리]**

* **해결** : 컬렉션 처리 캡슐화
* 일급 컬렉션 (First Calss Collection) : 컬렉션과 관련된 로직을 캡슐화 하는 디자인 패턴
* **조건**
  1. 컬렉션 자료형의 인스턴스 변수
  2. 컬렉션 자료형의 인스턴스 변수에 잘못된 값이 할당되지 않게 막고, 정상적으로 조작하는 메서드
* 외부에서 컬렉션의 조작 막기 (불변성 보장하기)
  * 배열 복사
  * `Object.freeze`

***

#### <mark style="background-color:red;">8장. 강한 결합: 복잡하게 얽혀서 풀 수 없는 구조</mark>

`요약 : 약한 결합 👍🏻`

* `강한 결합 (tughtly coupling)` : 클래스에 다른 클래스를 많이 의존하고 있는 구조 (지양)
* `약한 결합 (loose coupling)` : 결합도가 낮은 구조 (지향)

**\[강한 결합이 발생하는 구조]**

*   **상속 구조 :** 상속 구조는 강한 결합을 유발할 수 있음.

    *   서브 클래스는 슈퍼 클래스에 크게 의존하게 됨.

        → 서브 클래스에서 슈퍼 클래스의 구조를 하나하나 신경써야 하는 문제 발생.
    * 슈퍼 클래스가 공통 로직을 두는 장소로 사용될 수 있음.

    → 일반화는 강한 결합이 발생함.

    * **해결**
      * 컴포지션 사용 (private 인스턴스 변수 사용)
      * 단일 책임 원칙 지키기
        * 인스턴스별로 클래스 분할이 가능한 로직 : 메서드별로 클래스로 분리
      * 접근 수식자로 가시성 제어하기
      *   ts의 접근 제한자

          * 접근 제한자를 생략한 클래스 프로퍼티와 메서드는 `public`이 선언된다.

          <figure><img src="../../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

          * 참고 : private 메서드가 많으면 책임이 많아짐. → 책임이 다른 클래스로 분리
* 응집도가 높은 구조(데이터와 논리를 한 곳에 모은 구조)
  * 잘못 이해하여 강한 결합이 발생할 수 있음
  * **해결** : 각 개념을 각 클래스에 잘 분할하여 설계하기
*   **스마트 UI :** 화면 표시를 담당하는 클래스 중, 화면 표시화 직접적인 관련이 없는 책무가 구현된 클래스

    * **해결** : view - logic 분리하기

    ***
* **거대 데이터 클래스** : 수많은 인스턴스 변수를 가진 클래스
  * 다양한 데이터를 가져서 수많은 유스케이스에서 사용됨 -> 전역 변수와 같은 문제가 발생할 가능성이 높아진다
* **트랜잭션 스크립트 패턴** : 내부 일련의 처리가 하나하나 길게 작성되어 있는 구조
  * 메서드 하나가 수백 줄의 거대한 로직을 갖게되어, 응집도는 낮아지고 결합은 강해져 변경하기 어려운 코드가 됨.
*   **갓클래스** : 트랜잭션 스크립트 패턴 레벨업 버전

    * 수천\~수만줄의 로직을 담고 수많은 책임을 담당하는 로직이 섞여있는 클래스

    ***

**⇒ 해결** : 책임별 클래스 분리!!



### **Discussion Points**

Q. 일급 컬렉션에서 newMember의 어떤 특성에 따라 Member를 추가해야하는 기준이 다르다면, 이 부분은 Party가 아닌, 호출처에서 판단해야하는 영역일까? 여러 add가 생겨나야하는 것일까? 내부 add에서 전략패턴 혹은 팩토리 패턴을 이용하여 구분 처리하는 로직이 들어가는게 맞을까?

```typescript
// 이렇게 코드를 작성하면 기존 members를 변화시키지 않아서, Side Effect를 막을 수 있다.

class Member {
  constructor(public name: string) {}
}

class Party {
  private readonly members: Member[];

  constructor(members: Member[] = []) {
    this.members = [...members];
  }

  add(newMember: Member): Party {
    const adding = [...this.members, newMember];
    return new Party(adding);
  }
}
```



### **Apply**

외부에서 컬렉션의 조작 막기

* `Object.freeze`로 객체의 프로퍼티 불변을 보장

```typescript
const ViewPropsConstants = {
    TITLE_BAR_HEIGHT: 38,
    DEFAULT_LNB_WIDTH: 240,
    DEFAULT_RNB_WIDTH: 260,
    DEFAULT_GNB_HEIGHT: 56,
    ...
};

export default Object.freeze(ViewPropsConstants);
```



### Retrospective

컬렉션 중첩을 최소화하고 일급 컬렉션으로 관련 로직을 캡슐화하여 응집도를 높이는 것이 효과적이다.
