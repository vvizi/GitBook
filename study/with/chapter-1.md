---
description: 2024.05.17
---

# Chapter 1

#### <mark style="background-color:red;">**1장. 들어가며**</mark>

**웹 등장 배경 및 용어**

* **polyfill**
  * 브라우저가 지원하지 않는 코드를 브라우저에서 사용할 수 있도록 변환한 코드조각 및 플러그인. (`core.js`, `polyfill.io`)
* **transpile**
  * 최신 버전의 코드를 예전 버전의 코드로 변환하는 과정 (`Babel`)

→ jQuery 같은 브라우저 호환성을 해결해 주는 라이브러리가 있지만, 모든 크로스 브라우징 이슈를 해결할 수 없었음

→ 따라서 표준화된 자바스크립트가 필요하게 됨 : ECMA



* **웹 사이트**
  * HTML에 링크가 연결된 웹 페이지 모음. 콘텐츠가 동적으로 업데이트 되지 않음
* **웹 애플리케이션**
  * 사용자와 상호작용하는 웹. (검색, 댓글, 채팅 등 기능)
*   **Ajax**

    페이지를 새로고침 하지 않아도 js 비동기 요청으로 페이지 데이터를 로드할 수 있는 기법
*   **CBD (Component Based Development)**

    * 재사용할 수 있는 컴포넌트를 개발 또는 조합해 하나의 애플리케이션을 만드는 개발 방법론. 모듈과 달리 런타임 환경에서 독립적으로 배포, 실행될 수 있다.



**배민에서의 React + TS 도입 배경**

*   **배민에서 React + TS를 도입한 이유** : 좋은 제품을 제공하기 위해

    1. 성능과 확장성 보장
    2. 안정적이고 신뢰성이 높음
    3. 가독성이 높고 유지 보수성이 좋음


*   **React 선택 이유 :** 프레임워크가 아닌 라이브러리여서.

    1. 기술 스택 선택의 자유로움
    2. 컴포넌트 단위 개발에 적함
    3. 다양한 라이브러리, 프레임워크 접목 가능
    4. 가벼운 뷰 렌더링 사용에도 적절


*   **TS 선택 이유** : JS 표준을 지원하며 그 영역을 확장하는 것이 목적이기 때문

    1. OOP 지원 : 객체지향 프로그래밍 환경을 제공하여 복잡한 개발에 유리
    2. 강력한 생태계
    3. Server/Client 지원
    4. 디버깅 빠름
    5. 호이스팅, 형변환 등 복잡성 해결


* **배민이 프로젝트의 기술 스택을 적용하기 위해 노력한 점** (<mark style="color:red;">인상 깊은 부분</mark>)
  1. 프로젝트 진행 전 프로토타이핑과 코드리뷰 무한 반복
  2. 점심 시간마다 진행한 팀 내 스터디
  3. 해당 스택의 특성을 이해하고 잘 활용하는 것을 목표로 설정
  4. 과정의 공유와 피드백
  5. 도입 배경의 무한 리마인드