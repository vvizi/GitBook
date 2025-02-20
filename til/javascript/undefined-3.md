---
description: JS 엔진이 사용하지 않는 메모리를 자동으로 회수하는 기능
---

# 가비지 컬렉션

### 가비지 컬렉션이 필요한 이유

* 코드 실행 중에 생성된 변수, 객체, 함수는 메모리에 저장되지만 사용이 끝난 데이터는 **메모리 누수를 방지**하기 위해 자동으로 제거되어야 한다.
* 더 이상 도달할 수 없는 메모리를 탐지하여 해제해야 함.



### 매모리 관리 과정

1. 메모리 할당 : 변수/함수 선언, 객체 생성
2. 사용
3. 메모리 해제 : 더 이상 사용되지 않으면 메모리를 해제함.



### 도달 가능성

* 도달 가능한 객체
  * 전역 객체 : 브라우저 `window`, Node.js `global`
  * 콜 스택에 있는 모든 변수
  * 클로저를 통해 참조되는 변수
* 도달 불가능한 객체
  * 어떠한 참조도 받지 않는 객체



### 가비지 컬렉션 알고리즘

* Mark-and-Sweep&#x20;
  * 도달 가능한 객체에 Mark 표시
  * Mark되지 않은 객체를 메모리에서 제거



### 메모리 누수

사용하지 않는 객체가 메모리에 남아있는 상태

* 전역 변수의 사용
  * 애플리케이션이 종료될 때까지 해제되지 않음
  * 해결 : let, const 로 변수의 범위 제한하기, 모듈화와 함수 스코프를 활용
* 클로저에 의한 참조 유지
  * 클로저는 외부 변수에 대한 참조를 유지하므로, 필요하지 않은 외부 변수를 메모리에 계속 유지할 수 있다.
  * 해결 : 참조를 `null`로 설정하여 외부 변수의 참조를 해제
* DOM 요소 참조
  * `addEventListener` 로 이벤트 추가 시, 요소가 DOM에서 제거 되어도 해당 참조가 메모리에 유지된다.
  * 해결 : `removeEventListener` 로 이벤트 핸들러 제거, 일회성 이벤트 `once: true` 옵션 사용
* 순환 참조
  * 객체가 서로를 참조하는 경우, 참조를 해제하지 못한다.
  * 해결 : `WeakMap`, `WeakSet`, `WeakRef` 사용
    * **가비지 컬렉션에 의해 자동으로 제거**되는 객체 참조
* 타이머와 비동기 작업
  * `setTimeout` 또는 `setInterval`이 DOM 요소를 참조하면, 타이머가 제거되지 않는 한 메모리가 유지된다.
  * 해결 : 타이머가 더 이상 필요하지 않으면 `clearTimeout` , `clearInterval`로 해



### 요약

* 가비지 컬렉션은 **더 이상 사용되지 않는 메모리를 자동으로 회수**하여 메모리 누수를 방지한다.
* 메모리 누수는 전역 변수, 클로저, DOM 참조 및 순환 참조로 인해 발생할 수 있다.









