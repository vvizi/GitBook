---
description: 2024.04.02
---

# Chapter 13

### **Summary**

#### 13장 모델링 : 클래스 설계의 토대

`요약 : 설계는 한 번 했다고 끝나는 것이 아니라, 매일매일 반복해서 개선하는 것~`



**모델** : 특정 목적 달성을 위해 최소한으로 필요한 요소를 갖춘 것

* 목적을 알기 힘든 모델

<div align="left">

<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

</div>

* 목적별로 정의한 모델

<div align="left">

<figure><img src="../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

</div>

**악마를 불러들이기 쉬운 Class**

* 다양한 사양이 추가되어 모든 정보를 하나의 클래스 인스턴스 변수에 추가하는 class

→ 목적을 알기 힘든 모델

→ 목적별로 모델링 하기



**단일 책임이란 단일 목적이다.**

* 클래스가 이루어야 할 목적은 하나이다.



**모델을 다시 확인하는 방법**

* 해당 모델이 달성하려는 **목적**을 모두 찾아낸다.
* **목적별**로 모델링을 다시 **수정**한다.
* **목적 중심 이름 설계**를 기반으로 모델에 이름을 붙인다.
* 모델에 목적 **이외의 요소**가 들어가 있다면 **다시 수정**한다.



**모델과 구현은 반드시 서로 피드백 하기**

*   모델을 기반으로 클래스를 설계하고 , 코드를 구현하면서 세부적인 내용을 수정해야 한다.

    * 모델 !== 클래스
    * 모델 하나는 여러 개의 클래스로 구현된다.



**기능성을 좌우하는 모델링**

* 숨어있는 목적 파악하기
  * 개념의 정체와 뒤에 숨어있는 중요한 목적을 잘 파악해야 한다.



### **Discussion Points**

Q. _목적 중심으로 이름을 잘 설계하면, 목적을 달성하기에 적절한 모델을 설계할 수 있습니다._

→ 그렇다면 이미 구현된 코드를 리팩토링할 때, 해당 코드가 이루려는 목적을 나열하고 목적에 따라 모델링을 다시 해볼 수 있지 않을까? 🤔



Q. 목적별로 Class를 나누면 컴포넌트의 전역 상태를 관리하는 Class가 여러 개로 분산될 수 있다. 그렇다면 응집도를 위해 하나의 Class에서 관리하는 것이 더 좋은 방식이  아닐까?

A. 응집도를 나누는 기준에 따라 달라질 수 있을 것 같다.

* 전역 상태의 **목적**과 **변화 패턴**에 따라 Class 분리
* 관련된 모든 상태를 하나의 Class에서 관리하여 **응집도를 높이고** 구조를 단순화 하기기

### **Apply**

UI 요소를 관리하던 Class를 UI 별(컴포넌트 별)로 분리하기

```typescript
// UI Store 의 생성자

// Before
constructor() {
        makeObservable(this);
        this.GNB = true;
        this.LNB = true;
        this.RNB = true;
        this.saveStep = null;
        this.editObject = undefined;
        ...
    }

// After
    constructor() {
        makeObservable(this);
        this.objectUIContainer = new OSObjectUIContainer();
        this.viewPropsManager = new ViewPropsManager();
        ...
    }
```



### Retrospective

**응집도**와 **목적 중심의 분리** 간의 균형 고민하기.

* 전역 상태를 하나의 Class에서 관리하면 구조가 단순해지고 응집도가 높아지지만, 너무 많은 책임을 부여하면 Class가 비대해지고 유지보수에 어려움을 겪을 수 있기 때문.
