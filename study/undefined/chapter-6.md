---
description: 2024.02.15
---

# Chapter 6

### **Summary**

#### <mark style="background-color:red;">6장. 조건 분기 : 미궁처럼 복잡한 분기 처리를 무너뜨리는 방법</mark>

`요약 : 조건 분기는 지양하기`

**\[조건 분기]**

* **if 중첩, if-else의 문제점** : 코드의 가독성이 떨어짐-
* **해결** : 조기리턴(early return) -> 조건 로직과 실행 로직을 분리할 수 있다.
* **switch-case의 문제점**
  * 같은 형태의 조건문이 늘어남 따라 누락되는 부분이 생길 수 있음.
  * 유지보수의 어려움
* **해결** : 단일 책임 원칙
  * switch 조건문을 한 곳에서 구현 (같은 조건 분기를 여러 번 작성하지 말고 한 번에 작성)
  * Map으로 구현

***

**\[조건 분기 대체 방안 ]**

* **인터페이스 활용 :** 서로 다른 자료형을 같은 자료형처럼 사용할 수 있게 함
  * 다른 로직을 같은 방식으로 처리할 수 있다. (**전략 패턴:** 알고리즘을 정의하고 각각을 캡슐화하여 그들이 서로 바꿔 사용될 수 있도록 만드는 패턴)
* **정책패턴** : 같은 판정과 로직을 재사용
  * 조건을 부품처럼 만들어 조건을 조합해서 사용하는 패턴
* **자료형 확인**을 조건 분기에 사용하지 않기
  * ex. `instanceof Class`
  * 조건분기 중복되는 문제 초래 (**리스코프 치환 원칙 위반** - 자식 객체가 부모 객체를 완전히 대체할 수 있다는 원칙)
*   **플래그 매개변수** : 메서드의 기능을 전환하는 boolean 자료형의 매개변수

    * falg로의 조건 분기는 로직을 파악해야하기 때문에 동작을 예측하기 어렵다.
    * **해결** : 메서드 분리하기 (기능별로 분리)



### **Discussion Points**

Q. 코드블록 `{ }` 없이 한 줄로 작성하는 if문은 가독성이 좋은 걸까요?

A. _코드블록 { }_ 없이 한 줄로 작성하는 if문은 개인적으로 가독성이 저하된다고 생각합니다.  또한 실행 로직이 늘어날 때는 실수할 수 있는 확률도 높아질 수 있습니다.

```jsx
if (a>b) return true;
```



### **Apply**

**자료형 확인**을 조건 분기에 사용하지 않기

*   나름대로 생각한 해결 방안 - **사용자 정의 타입가드**

    ```jsx
    // class의 인스턴스를 확인하는 형태 
    export const getWidgetType = (selectedWidget: SelectedModel) => {
        if (selectedWidget instanceof WidgetModel) {
            return selectedWidget.getWidgetType();
        }
        return selectedWidget.getObjectType();
    };

    // 사용자 정의 타입가드 활용하기
    // getWidgetModelType 함수를 통해 어떤 타입인지 확인할 수 있다.
    export const isWidgetModel = (obj?: any): obj is WidgetModel => getWidgetModelType(obj);

    export const getWidgetType = (selectedWidget: SelectedModel) => {
        if (isWidgetModel(selectedWidget)) {
          return selectedWidget.getWidgetType();
        }
        return selectedWidget.getObjectType();
      }
    ```



### Retrospective

조건 분기 로직을 단순화하면 코드가 읽기도, 이해하기도 쉬워진다.
