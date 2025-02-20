---
description: 2024.03.15
---

# Chapter 10

### **Summary**

#### <mark style="background-color:red;">10장 이름 설계 : 구조를 파악할 수 있는 이름</mark>

`요약 : 구체적이고 의미 범위가 좁고 특화된 이름으로 짓기!`

이름 설계가 잘 못 되면, 강한 결합 구조를 갖게 된다. -> _관심&#xC0AC;_&#xC5D0; 따라서 각 클래스로 _분&#xD560;_&#xD574;야 한다.

**\[관심사 분리]**

* 관심사에 맞는 이름 붙이기
  * 이름별로 분할한 클래스 각각에 관심사에 맞는 로직을 캡슐화하기
* 포괄적이고 의미가 불분명한 이름
  * 너무 포괄적인 이름은 내부에 온갖 로직을 구현하게 만든다. -> 관심사 분리를 쉽게 하는 방법 : 비즈니스 목적에 따라 이름을 붙인다

**\[이름 설계하기 - 목적 중심 이름 설계]** 관심사 분리 및 비즈니스 목적에 맞게 이름을 붙이는 것은 결합이 느슨하고 응집도가 높은 구조를 만들 수 있다.

* 최대한 구체적이고 의미 범위가 좁고 특화된 이름 선택하기
  * 특화된 의미 범위가 좁은 이름을 클래스에 붙인다.
* 존재가 아니라 목적을 기반으로 하는 이름 생각하기
  * `ex. userName - accountName, nickName, realName ...`
* 어떤 비즈니스 목적(관심사)이 있는지 분석하기
  * 소프트웨어가 추구하는 목적과 내용을 분석한다.
  * `ex. 게임 : 무기, 몬스터, 아이템, 기간 이벤트 ....`
* 소리내어 이야기 해보기
  * `고무 오리 디버깅`: 어떤 문제가 발생했을 때, 책상 위의 오리 인형에게 문제를 처음부터 차근차근 설명해 보면서 해결하는 방법
* 이용 약관 읽어 보기
  * 이용 약관은 서비스와 관련된 규칙이 엄격한 표현으로 작성되어 있기 때문에 비즈니스와 관련된 이름을 알 수 있다.
* 다른 이름으로 대체할 수 없는지 검토하기
  * `ex. 고객 : 숙박하는 사람 / 결제하는 사람`
* 결합이 느슨하고 응집도가 높은 구조인지 검토하기
  * 의미가 더 좁은 특화된 이름 찾기

**\[이름 설계 시 주의 사항]**

* 이름에 관심 갖기
  * 이름과 로직을 대응해보기
* 사양 변경 시 '의미 범위 변경' 경계하기
  * 반복되는 사양 변경에 의해, 개발 맥락에서 말이 의미하는 바가 점점 변화하는 경우 주의
* 대화에는 등장하지만 코드에 등장하지 않는 이름 주의하기
  *   소스코드에 로직으로만 작성된 경우 주의

      → 로직을 찾는 일이 어려워짐

      → 이름을 기반으로 메서드와 클래스를 설계 필요
* 수식어를 붙여서 구별해야 하는 경우는 클래스로 만들어 보기
  *   의미가 다르거나 조건에 따라 달라지는 대상을 같은 이름으로 표현하면 차이를 구별하기 어렵다

      → 의미를 구분하기 위해 수식어를 붙임

      → 수식어를 붙이면서까지 차이를 나타내고 싶은 대상은 각 클래스로 설계하기

**\[의미를 알 수 없는 이름]**

이름의 의미를 알 수 없으면 책무를 알 수 없고, 강한 결합 구조가 되기 쉽다.

→ 의미를 해석하는데 오래 걸림

* 기술 중심 명명 : 비즈니스 목적을 나타내는 이름이 아닌, 기술 중심으로 서술한 이름 (`changeIntValue`등)
* 로직 구조를 나타내는 이름 : 대상이 무엇을 하려는지 제대로 이해하고 짓기
* 놀람 최소화 원칙 : 사용자가 예상하지 못한 놀라움을 최소화하도록 설계해야 한다는 접근 방법 → 로직과 이름을 잘 대응시켜야 한다.
  * 사양을 변경하면서, 기존 로직을 수정하게 되어 놀람 최소화 원칙을 위반하게 될 수 있음.

**\[구조에 악영할을 미치는 이름]**

* 데이터 클래스처럼 보이는 이름
* 클래스를 거대하게 만드는 이름
  * `Manager`, `Processor`, `Controller`라는 이름은 의미가 너무 넓다.
  * 많은 책무를 떠안아서 단일 책임 원칙을 위반할 수 있다.
* 상황에 따라 의미가 달라질 수 있는 이름
  * account는 권한, 계좌 등 여러 의미를 가질 수 있음
* 일련번호 명명 : 클래스 이름에 번호를 붙여 만드는 것
  * 목적과 의도를 알기 힘들고 구조를 개선하기가 훨씬 힘들다.
* 이름을 봤을 때, 위치가 부자연스러운 클래스
  * 관심사가 다른 메서드는 `동사+목적어` 형태가 되는 경향이 있다 → 관계없는 책무를 가진 메서드일 가능성이 높다
  * 영어로 읽어도 위화감 없는 클래스로 메서드를 정의해야 한다.

**\[이름 축약]**

* 의도를 알기 어렵게 이름이 축약되면 안된다.
* 이름을 축약하지 않는 게 좋다.
* 이름을 축약할 수 있는 경우
  * 카운터 변수 같은 `i`,`j`의 경우



### **Discussion Points**

Q. 여러 개의 룰로 이루어진 validate 함수를 util과 class 중 어느 것이 좋은 구조일까?

A1. 각 룰을 함수로 분리하여, 여러 개의 룰을 호출하는 util 함수로 작성

```typescript
// 명명 규칙을 검사하는 함수
function validateNamingRules(name: string): boolean {
    // 예시
    const isValid = /^[a-zA-Z]+$/g.test(name);
    if (!isValid) {
        throw new Error("Name does not follow the naming rules.");
    }
}

// 이름이 중복되었는지 검사하는 함수
function checkForDuplicate(name: string, isDuplicated: boolean): void {
    if (isDuplicated) {
        throw new Error("Name is duplicated.");
    }
}

// 이름 검증 프로세스를 관리
function validateName(name: string, isDuplicated: boolean): void {
    validateNamingRules(name); // 명명 규칙 검사
    checkForDuplicate(name, isDuplicated); // 중복 검사
    
    return true;
}
```

A2. 전략 패턴 및 복합 전략 패턴을 이용하여 class로 작성

```typescript
interface ValidationStrategy {
    validate(name: string, ...args: any[]): void;
}

class NamingRuleValidationStrategy implements ValidationStrategy {
    validate(name: string) {
		    // 예시
        const isValid = /^[a-zA-Z]+$/g.test(name);
        if (!isValid) {
            throw new Error("Name does not follow the naming rules.");
        }
    }
}

class DuplicateValidationStrategy implements ValidationStrategy {
    validate(name: string, isDuplicated: boolean) {
        if (isDuplicated) {
            throw new Error("Name is duplicated.");
        }
    }
}

class CompositeValidationStrategy implements ValidationStrategy {
    private strategies: ValidationStrategy[] = [];

    addStrategy(strategy: ValidationStrategy) {
        this.strategies.push(strategy);
    }

    validate(name: string, ...args: any[]) {
        this.strategies.forEach(strategy => {
            strategy.validate(name, ...args);
        });
    }
}

class Validator {
    private strategy: ValidationStrategy;

    constructor(strategy: ValidationStrategy) {
        this.strategy = strategy;
    }

    setStrategy(strategy: ValidationStrategy) {
        this.strategy = strategy;
    }

    validateName(name: string, ...args: any[]) {
        this.strategy.validate(name, ...args);
    }
}
```



### **Apply**

#### 리액트에서의 `validate` 함수 구조

리액트에서는 **util 함수**로 여러 개의 룰을 관리하는 방식이 더 간결하고 유지보수가 쉬울 수 있다.

1. **단순성**: 여러 개의 작은 유틸리티 함수로 분리하여 필요한 룰을 조합하거나 호출하는 방식이 코드 구조를 단순하게 한다.
2. **재사용성**: 함수 단위는 컴포넌트에서도 쉽게 재사용할 수 있다.
3. **경량성**: 클래스 기반 설계는 유지보수 및 코드 가독성에 유리할 수 있지만, 리액트에서는 클래스가 복잡성을 높일 수 있다.

### Retrospective <a href="#retrospective" id="retrospective"></a>

`Manager`, `Processor`, `Controller` 같은 이름을 자주 사용했지만, 더 구체적인 목적에 따라 명확히 분리하는 것이 좋은 구조로 가는 길이다.\
