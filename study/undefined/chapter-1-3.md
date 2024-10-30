---
description: 2024.01.19
---

# Chapter 1 \~ 3

### **Summary**

#### <mark style="background-color:red;">1장. 잘못된 구조의 문제 깨닫기</mark>

* 의도와 목적을 드러내는 이름 사용하기

_확인 버튼 클릭_ 이벤트에 대한 핸들러 함수를 작성한다고 했을 때, ‘의도와 목적을 잘 드러냈다’ 라는 기준이 고민된다.

`handleClick` : 클릭할 수 있는 개체가 유일할 때?

`handleButtonClick` : 클릭할 수 있는 개체 중에 유일한 버튼일 때?

`handleOKButtonClick` : 여러 버튼 중 ok?

* 중첩이 많을수록 코드의 가독성이 나빠진다.

[early-return 패턴](https://woonys.tistory.com/entry/Design-PatternJavaEarly-return-pattern%EC%9D%B4%EB%9E%80) 으로 처리하는 게 가독성을 높일 수 있다.

* 응집도가 낮은 구조 (데이터와 로직이 분산되어 있는 구조)는 많은 문제를 초래할 수 있다.
  * 코드 중복
  * 수정 누락
  * 가독성 저하
  * 초기화 되지 않은 객체
  * 잘못된 값 할당

#### <mark style="background-color:red;">2장. 설계 첫걸음</mark>

* 의도를 분명히 전달할 수 있는 이름으로 설계하기
  * 변수 이름을 쉽게, 의도를 쉽게 알 수 있는 이름 붙이기
* 의미있는 로직을 모아서 함수로 분리하기
* 관련된 데이터와 로직을 클래스로 모으기

> 응집도를 높이자 & 객체 지향 설계를 하자.

#### <mark style="background-color:red;">3장. 클래스 설계 : 모든 것과 연결되는 설계 기반</mark>

클래스 하나로도 잘 동작할 수 있도록 설계해야 한다.

* 클래스 전체가 에러나는 일 없이, 최소한의 조작방법(메서드)만 외부에 제공해야 한다.
  * 클래스 자체에서 초기화, 유효성 검사를 수행 필요.
* 성숙한 클래스로 성장시키는 설계 기법
  1. 생성자에서 초기화하기 및 생성자 내부에서 validation check
  2. 로직과 변수의 응집도 높은 구조로 구현.
  3. 불변 변수 만들기
     1. 값이 계속해서 바뀌면 디버깅이 어렵고, side effect 가 발생할 수 있다.
  4. 값을 변경하기 위한 목적이라면 새로운 인스턴스를 만든다.
  5. 메서드의 매개변수와 지역변수는 불변으로 만든다.
  6. 잘못된 값을 전달하지 않는다 (타입 체크)
  7. 의미 없는 메서드를 추가하지 않는다.



### Discussion Points

Q. 어떠한 상태를 관리하거나 필요로 하지 않는다면, 클래스 대신 순수함수를 사용해 util로 분리하는 구조는 어떨까요??

A1. 응집도가 낮아질 수 있음

A2. 함수형 프로그래밍에선 util이 응집도를 높이는 방법일 수 있음



### Apply

중첩이 많을수록 코드의 가독성이 나빠진다.

* early-return 패턴 적용

```tsx
onChange={selectedOption => {
         setHeaderKeyFilter(selectedOption);

         if (headerListIsValid(headerDataList, selectedOption)) {
                handleKeyChange(selectedOption);
         } else {
                handleKeyChange('');
                setOpenSnackbar(true);
          }
}}
```

```tsx
onChange={selectedOption => {
    setHeaderKeyFilter(selectedOption);

    if (headerListIsValid(headerDataList, selectedOption)) {
        handleKeyChange(selectedOption);
        return;
    }

    handleKeyChange('');
    setOpenSnackbar(true);
}}
```



### Retrospective

* 1,2,3장의 내용은 _값 객체_ 디자인 패턴(즉, 응집도를 높이는 구조)가 안전하고 잘 설계된 구조라고 말한다.
  * p35 ‘객체 지향을 활용한 설계 효과 검증’ 표를 참고하여, 스스로 설계 검증을 하면 좋을 듯.
* 평소에는 `button`, `label`처럼 간단한 명명을 선호했지만, 이런 간단한 명명도 코드 퀄리티에 영향을 줄 수 있음을 깨달아 앞으로는 더 신중하게 접근하고자 한다.
