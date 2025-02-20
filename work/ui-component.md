---
description: 2024.06 - 2024.10
---

# 디자인 시스템 기반 공통 UI 컴포넌트 라이브러리 구축

### **Description**

디자인팀의 디자인 시스템을 기반으로, 다양한 **공용 UI 컴포넌트**(dialog, dropdown 등)를 클린 코드와 웹 접근성을 고려해 **재사용 가능한 구조로 개발**했습니다.

* **사업명** : Tmax Gaia
* **고객사** : 포스코(도시락 서비스), 미래엔(디지털 교과서) / 2,000명 규모 사내 계열사
* **참여 인원** : <mark style="color:blue;">개발 1명</mark> / 기획 2명 / 디자인 2명
* **역할** : UI 개발 / <mark style="color:blue;">기여도 100%</mark>
* **성과** : 100명 이상의 코드베이스의 **디자인 시스템 체계 구축** 및 **라이브러리 확립**



### Goals.

1. **일관된 사용자 경험 제공** : 공용 UI 컴포넌트를 통해 사용자 경험을 통일해 브랜드 일관성을 유지한다.
2. **개발 효율성 향상** : 재사용 가능한 컴포넌트를 제공하여 개발 속도를 높이고 코드 중복을 줄인다.
3. **유지보수 강화** : 규격화된 디자인 시스템을 통해 컴포넌트 수정 시 전체 시스템에 일괄 반영한다.



### How to.

**단일 책임 원칙 준수 :** 기능을 분리하고 체계적인 구조로 컴포넌트를 구성했습니다.

**Context API와 Hooks 활용:** 전역 상태 관리가 필요한 경우 Context API를 사용해 불필요한 props drilling을 방지합니다. 공통 로직은 커스텀 Hooks로 분리하여 코드의 가독성과 유지보수성을 강화합니다.

**접근성과 웹 표준 준수 :** 스크린 리더 사용자를 위해 ARIA 속성을 적용했습니다.

**Storybook으로 컴포넌트 문서화:** Storybook을 통해 컴포넌트별 사용법, Props 설명, 코드 예시를 제공하여 팀원들이 쉽게 이해하고 사용할 수 있도록 했습니다.

<figure><img src="../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

**Code Base1** : **웹 접근성**과 **웹 표준**을 준수하였습니다.

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

**CodeBase2** :  **비즈니스 로직과 UI 로직을 분리**하였습니다.

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption><p>Notification의 비즈니스 로직 NotificationContainer</p></figcaption></figure>

**CodeBase3 :** `will-change: transform, opacity;` 속성으로 성능을 최적화하고, `@mixin`으로 스타일 재사용성을 높였습니다

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption><p>Notification.scss</p></figcaption></figure>



**협업 도구** : 협업을 위한 **사용 가이드** 및 **StoryBook**을 작성하여 팀에 공유하고 안내했습니다.

문서화로 컴포넌트를 테스트하고 협업 환경을 개선할 수 있었습니다.



<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption><p>GitLab Wiki</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption><p>StoryBook</p></figcaption></figure>

### Result.

> 프로덕션에 적용된 컴포넌트 영상

{% file src="../.gitbook/assets/notification.mp4" %}

{% file src="../.gitbook/assets/switch.mp4" %}
