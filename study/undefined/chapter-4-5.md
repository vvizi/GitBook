---
description: 2024.02.08
---

# Chapter 4 \~ 5

### **Summary**

#### <mark style="background-color:red;">4장. 불변 활용하기 : 안정적으로 동작하게 만들기</mark>

`요약 : 예측 가능한 코드로 작성하자`

*   **재할당**은 변수의 의미를 바꿔 **의미를 추측 & 값을 추적**하기 어렵게 한다.

    → 변수 재활용 ❌ / 새로운 변수 ⭕

    → 불변 변수로 만들어 재할당 막기 `const`


*   **매개변수**도 **불변**으로 막기

    → TypeScript의 매개변수는 기본적으로 재할당이 불가능

    (단, 매개변수가 객체(배열)과 같은 참조 타입일 경우, 해당 **객체의 속성**은 변경할 수 있음)
* 가변적인 구조는 부수효과를 주기 쉽다.
  * 유지보수 어려움
  * 버그 발생
* 해결방안
  * 함수의 영향 범위 한정하기
    * 데이터(상태)는 매개변수로 받기
    * 상태 변경하지 않기
    * 값은 함수의 리턴 값으로 돌려주기
  * 불변으로 만들기
  * 코드 외부와 데이터 교환 시, 리포지토리 패턴 사용 권장

***

#### <mark style="background-color:red;">5장. 응집도 : 흩어져 있는 것들</mark>

`요약 : 코드의 분산을 해결하자`

* 응집도가 **높은** 구조 : 구조를 변경하기 쉬움
* 응집도가 **낮은** 구조 : 구조 변경 시 문제가 발생하기 쉬움
  * 코드가 분산되어 있으면, 어떤 코드가 어디 있는지 알기 힘듦
*   `static` 메서드로 정의하기

    **장점**

    * 코드 중복을 줄일 수 있다.
    * 클래스의 인스턴스를 생성하지 않고도, 메서드를 호출할 수 있다.

    **단점**

    * 데이터와 로직이 다른 클래스에 정의될 수 있음. (낮은 응집도)
* 생성 로직이 많아지면 **팩토리 클래스**를 고려하자
* **범용 처리 클래스** (common, util) 사용 범위 : 횡단 관심사
  * 로그출력, 오류 확인, 디버깅, 예외 처리, 캐시, 동기화, 분산 처리 같은 기능들
* 매개변수가 많아지면 로직이 복잡해지거나 중복코드가 생길 가능성이 높아짐
  * 매개변수 데이터를 인스턴스 변수로 갖는 클래스를 만들자
* 매개변수로 기본 자료형이 아닌, **클래스 자체**를 받아도 응집도를 높일 수 있음

### Discussion Points

Q. 우리 프로젝트에 수 많은 Util 함수가 존재하는데, 이 중에 횡단 관심사에 해당하는 것들은 무엇이 있을까요?

A. 디버깅 관련 util, time 관련 util...&#x20;



### Apply

가변적구조를 불변적 구조로  바꾸어 프로덕션 코드에 적용

*   let 예시

    함수화 하여 조건부 반환으로 처리할 수 있다. (즉시 실행 함수 등)

    <pre class="language-jsx"><code class="lang-jsx"><strong>// Before
    </strong><strong>let value;
    </strong>if (condition) {
        value = 'A';
    } else {
        value = 'B';
    }
    </code></pre>

    ```jsx
    // After : 나름대로 생각한 해결법
    const getValue = (condition) => {
        if (condition) {
            return 'A';
        } 
      return 'B';
    }
    const value = getValue(condition);
    ```
*   재할당이 가능한 매개변수 예시

    ```jsx
    // Before
    function getTime(item: Model): string{
    item.timestamp = '2024';
    ```

    ```jsx
    // After : 나름대로 생각한 해결법
    const { timestamp } = item;
    const timeAgo = getTimeAgo(timestamp);
    ```

### Retrospective

`Hook`, `class`, `util`의 적절한 사용 시점과 활용 방안을 더욱 깊이 고민할 필요가 있음을 느꼈다.

