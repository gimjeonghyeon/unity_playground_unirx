# UniRx란?

---

- UniRx는 Unity에서 사용되는 Reactive Extensions (Rx) 패턴을 구현한 라이브러리이다.
- Rx 패턴은 비동기 이벤트 및 데이터 스트림을 처리하는데 사용된다.
- UniRx는 개발자가 이러한 패턴을 개발에 쉽게 활용할 수 있도록 만든 라이브러리가 UniRx이다.


💡 **.Net용 Rx를 사용하지 않는 이유는?**
```
- .Net용 Rx는 Mono의 .Net 버전 문제로 사용이 불가능
- 또한 .Net용 Rx는 크고 무거움
```

# UniRx를 사용해야하는 이유

---

### 비동기 작업 관리

- UniRx를 사용하면 Unity에서 타이머, 애니메이션, 입력 이벤트, 네트워크 통신 등의 다양한 비동기 작업을 효과적으로 처리하고 관리할 수 있습니다.
- 유니티에서 Coroutine을 이용한 비동기 처리시 발생하는 다음과 같은 단점을 해결할 수 있습니다.
    - 값을 반환할 수 없음 (IEnumerator를 반환해야하기 때문에)
    - 예외처리를 할 수 없음 (yield return 문을 try-catch로 감쌀 수 없기 때문에)
- 또한 시간의 처리가 간단해집니다.
    - 이벤트의 기다림 (마우스 클릭 또는 버튼의 입력)
    - 비동기 처리 (통신 또는 데이터 로드)
    - 시간 측정이 판정에 필요한 처리 (홀드, 더블클릭 판정)
    - 변화하는 값의 감시 (false가 true가 되는 순간 1회만 처리)

### UI업데이트와 통합

- UniRx는 UI 요소와 데이터 스트림을 바인딩하고 데이터 변경시 자동으로 UI를 업데이트 하는 등 UI 업데이트와 통합하기에 용이합니다.

# UniRx 동작을 3단계로 나눈다면

---

1. 스트림 생성
2. 오퍼레이터를 사용하여 스트림 가공
3. 가공된 스트림을 구독하여 사용

💡 **스트림이란?**
```
- 타임라인에 배열되어 있는 이벤트의 시퀀스 (연속적인 이벤트의 흐름)
- 분기되거나 병합하는 것이 가능
- 코드 안에서는 IObservable<T> 로 취급 (IObservable<T> 로 구독이 가능하다)
```

# 주요 개념

---

### Observable

- 비동기 데이터 스트림
- 시간에 따라 데이터를 내보내는 객체로 볼 수 있음
- 사용자 입력, 이벤트, 센서 데이터 등을 스트림으로 다룰 수 있음

### Observer

- Observable을 구독하고 Observable에서 발생하는 이벤트나 데이터를 처리
- Observable로부터 데이터를 받아볼 수 있으며, 데이터에 반응하여 작업을 수행 가능

### Operators

- UniRx에서 제공하는 다양한 연사자로 Observable의 데이터 스트림을 조적하고 변환할 수 있게 함
- 필터링, 매핑, 결합, 그룹화, 시간지연등의 기능 제공

# 메시지

---

스트림에 흐르는 이벤트(스트림에 발행되는 메시지)

- OnNext
    - 일반적으로 사용되는 메시지
- OnError
    - 에러 발생시에 예외를 통지하는 메시지
    - 구독자에게 도달한 순간 구독이 종료된다.
- OnComplete
    - 스트림이 완료되었음을 통지하는 메시지, 해당 메시지를 받으면 스트림이 종료된다.
    - 정적 스트림의 경우 OnCompleted를 받을 때까지
- IObserver
    - 메시지 발행을 위한 인터페이스

# 구독

---

- 스트림은 Subcribe 된 순간에 생성된다
- 기본적으로 Subcribe 하지 않은 스트림은 동작하지 않는다
- Subscribe 타이밍에 의해서 결과가 바뀔 가능성이 있다
- OnError, OnComplete 가 오면 Subcribe는 종료된다.
- Subcribe는 오버로드로 여러 개 정의되어 있어서, 용도에 따라 사용하는게 좋다
    - OnNext만
    - OnNext & OnComplte
    - OnNext & OnError & OnCompleted
- IObservable
    - 메시지 구독을 위한 인터페이스

# Subject

---

- UniRx에서 제공하는 Subject<T> 를 통해 UniRx 스트림을 생성할 수 있다.
- ISubject는 IObservable과 IObserver를 구현하고 있다.
    - subject 객체에서 OnNext(), OnComplete(), OnError() 메시지를 직접 호출할 수 있다.

# 오퍼레이터

---

- Drag 관련 속성
    - OnBeginDragAsObservable
    - OnDragAsObservable
    - OnEndDragAsObservable

# 참고

---

[[160402_데브루키_박민근] UniRx 소개](https://www.slideshare.net/agebreak/160402-unirx)

[2022년 현재 UniRx의 용도 | Lonpeach Tech](https://tech.lonpeach.com/2022/10/29/2022-unirx/)

[Reactive Programming(리액티브 프로그래밍) - RxJava란](https://velog.io/@salgu1998/Reactive-Programming리액티브-프로그래밍-이란)
