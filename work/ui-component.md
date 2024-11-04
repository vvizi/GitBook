---
description: 2024.06 - 2024.10
---

# 공용 UI Component

### **Description**

디자인팀의 GUI 가이드를 기반으로, 다양한 **공용 UI 컴포넌트**(dialog, dropdown 등 **28종**)를 클린 코드와 웹 접근성을 고려해 **재사용 가능한 구조로 개발**했습니다.

* **사업명** : Tmax Gaia
* **고객사** : 사내 계열사
* **참여 인원** : <mark style="color:blue;">개발 1명</mark> / 기획 2명 / 디자인 2명
* **역할** : UI 개발 / <mark style="color:blue;">기여도 100%</mark>
* **성과** : 디자인 시스템 체계 구축 및 개발 시간 단축



### Goals.

1. **일관된 사용자 경험 제공** : 공용 UI 컴포넌트를 통해 사용자 경험을 통일해 브랜드 일관성을 유지한다.
2. **개발 효율성 향상** : 재사용 가능한 컴포넌트를 제공하여 개발 속도를 높이고 코드 중복을 줄인다.
3. **유지보수 강화** : 규격화된 디자인 시스템을 통해 컴포넌트 수정 시 전체 시스템에 일괄 반영한다.



### How to.

**설계** : 컴포넌트 구조화

**단일 책임 원칙**을 적용하여, 기능을 분리하고 체계적인 구조로 컴포넌트를 구성했습니다.

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
