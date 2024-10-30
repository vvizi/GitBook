---
description: 2024.07.24
---

# Chapter 9\~10

<mark style="background-color:red;">**9장. 훅**</mark>

훅이 도입되면서 클래스 컴포넌트와 같이 컴포넌트의 생명주기에 맞춰 로직을 실행할 수 있게 되었음.

\-> 비즈니스 로직 재사용

\-> 코드 분할 및 테스트 가능

\-> 사이드 이펙트와 상태를 관심사에 맞게 분리하여 구성 가능

* 훅은 호출 순서에 의존한다.



**\[useState]**

반환 타입 : `[S, Dispatch<SetStateAction>]`; 튜플&#x20;

S : 제네릭

Dispatch : 상태를 업데이트할 수 있는 타입의 함수



**\[의존성 배열을 사용하는 훅]**

`useEffect, useLayoutEffect`

* useEffect의 첫 번째 인자이자 타입인 EffectCalllback은 Destructor를 반환하거나 아무 것도 반환하지 않는다.
* useEffect의 콜백함수로 비동기 함수를 호출할 수 없다.
* useEffect deps는 얕은 비교로만 판단하기 때문에, 실제 객체 값이 바뀌지 않았더라도, 객체의 참조 값이 바뀌면 콜백 함수가 실행된다.
* \[] 빈 배열 : 컴포넌트가 처음 렌더링될 때만 실행한다.
* 배열 존재 : 배열 값이 변경될 때마다 Destructor(Cleanup 함수) 실행

`useLayoutEffect` : 레이아웃 배치와 화면 렌더링이 모두 완료된 후에 실행된다. 화면에 그려지기 전에 콜백 함수를 실행함.



**\[useMemo와 useCallback]**

* 이전에 생성된 값, 함수를 기억하며 동일한 값과 함수를 반복해서 생성하지 않도록 해준다.
* 값을 계산하는 데 오랜 시간이 걸릴 때나 렌더링이 자주 발생하는 form에서 사용한다.



**\[useRef]**

DOM을 직접 선택해야하는 경우

ref를 props으로 전달하기 위해서는 `forwardRef`를 사용



**\[useImpreativeHandle]**

`ForwardRedRenderFunction`과 함께 쓸 수 있는 훅

ref를 통해서 자식 컴포넌트에서 정의한 커스터마이징된 메서드를 호출할 수 있다.

\-> 자식 컴포넌트는 내부 상태나 로직을 관리하면서 부모 컴포넌트와의 결합도도 낮출 수 있다.

* 값이 바뀌어도 컴포넌트의 리렌더링이 발생하지 않는다.
* 상태 변경 함수를 호출하고 렌더링된 이후에 업데이트된 상태를 조회할 수 있다.



<mark style="background-color:red;">**10장 상태관리**</mark>

**상태(State)** : 렌더링에 영향을 줄 수 있는 동적인 데이터 값

* 지역 상태 / 전역 상태 / 서버 상태

**지역 상태**

useState, useReducer 와 같은 훅이 사용됨

**전역 상태**&#x20;

prop drilling을 피하고 컴포넌트들 사이의 전역 상태로 공유할 수도 있다.

서버 상태 서버에서 관리하는 상태, react-query, SWR과 같은 외부 라이브러리를 사용

상태가 없는 Stateless 컴포넌트를 활용하자

1. 시간이 지나도 변하지 않는다면 상태가 아니다.

* 객체 참조 동일성을 유지하는 방법을 고려하자. (메모이제이션)
* useMemo를 통한 메모이제이션은 의미상 보장된 것 X -> 성능상 이점
* `const [store] = useState(() => new Store());`

2. 파생된 값은 상태가 아니다.

* **SSOT(single source of truth)** 는 어떠한 데이터도 단 하나의 출처에서 생성하고 수정해야 한다는 원칙
* props는 상태가 아니다.



**\[useState vs useReducer]**

\->`useReducer` 권장

**이유 1.** 다수 하위 필드를 포함하고 있는 복잡한 로딩을 다룰 때

**이유 2**. 다음 상태가 이전 상태에 의존적일 때



**\[전역 상태 관리와 상태 관리 라이브러리]**

* 상태는 사용하는 곳과 최대한 가까워야 하며 사용 범위를 제한해야만 한다.
  * `Context API + useState/useReducer`  외부 상태 관리 라이브러리



**Context API**

상위 컴포넌트의 Context를 하위 컴포넌트에서 구독하는 형식

**단점.** `context provider`로 주입된 값이나 참조가 바뀌면 하위 모든 컴포넌트가 리렌더 된다.



