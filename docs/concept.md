# Sync & Async, Blocking & Non-Blocking

동기 & 비동기 통신과 Blocking, Non-blocking 개념에 대한 정리입니다.

## Synchronous & Asynchronous

### Definition

- **Synchronous**: 동기 통신으로, 요청과 응답이 순서를 가진다.
- **Asynchronous**: 비동기 통신으로, 요청과 응답이 순서 없이 이루어진다.

### Difference

한 함수가 다른 함수를 호출하여 작업을 진행하는 과정에서 **작업의 완료 여부를 어떤 함수가 신경쓰는지**에 차이가 있다.

- **Synchronous**

    - 호출하는 함수는 호출된 함수의 작업 완료를 확인하며 기다린다.
        > 이 때 작업이 완료될 때 까지 대기하거나 다른 작업을 할 수 있다.
    - 호출된 함수의 작업이 완료되면 호출한 함수가 바로 결과를 처리한다.

    ```
    A 함수가 B 함수 호출
    -> B 함수 작업 완료
    -> B 함수가 A 함수에게 결과 반환
    -> A 함수가 바로 처리
    ```

- **Asynchronous**

    - 호출된 함수는 호출한 함수에게 Callback 을 반환한다.
    - 호출한 함수는 작업의 완료를 신경쓰지 않기 때문에, 결과를 바로 처리하지 않는다.

    ```
    A 함수가 B 함수 호출
    -> B 함수가 A 함수에게 콜백 반환
    -> B 함수가 A 함수에게 작업 완료 알림
    -> A 함수가 나중에 처리
    ```

## Blocking & Non-Blocking

### Definition

- **Blocking**: 요청 후 응답까지 대기하는 방식
- **Non-Blocking**: 요청 후 응답까지 다른 작업을 진행하는 방식

### Difference

한 함수가 다른 함수를 호출하여 작업을 진행하는 과정에서 **작업의 제어권이 어떤 함수에 있는지**에 차이가 있다.

- **Blocking**

    - 호출된 함수의 작업이 완료될 때 까지 제어권은 호출된 함수에게 있다.
    - 호출한 함수는 호출된 함수의 작업 완료를 기다린다.

    ```
    A 함수가 B 함수 호출
    -> B 함수가 제어권 소유
    -> A 함수 대기
    -> B 함수가 작업 완료 후 A 함수에게 제어권 반환
    ```

-  **Non-Blocking**

    - 호출된 함수는 즉시 호출한 함수에게 제어권을 반환한다.
    - 호출한 함수는 작업 완료에 관계 없이 다른 작업을 진행할 수 있다.

    ```
    A 함수가 B 함수 호출
    -> B 함수가 A 함수에게 제어권 반환
    -> A 함수가 제어권 소유
    -> A 함수는 다른 작업 진행
    ```

## Design & Performance

**Synchronous & Asynchronous** 개념은 시스템의 설계와 관련이 있으며, **Blocking & Non-Blocking** 개념은 성능에 중요한 영향을 준다.

### Synchronous & Asynchronous

- **Synchronous**: 요청과 응답이 순서대로 이루어지기 때문에 더 간단한 시스템을 설계할 수 있다.
- **Asynchronous**: 요청과 응답에 순서가 없는 복잡한 시스템을 설계할 수 있다.

### Blocking & Non-Blocking

- **Blocking**: 다른 작업의 완료를 대기해야 하기 때문에 성능이 더 느려진다.
- **Non-Blocking**: 여러 작업을 효율적으로 처리할 수 있어 성능이 향상된다.

## Pros & Cons

일반적으로 사용되는 **Sync & Blocking** 과 **Async & Non-Blocking** 기법은 각각 뚜렷한 장단점이 있고, 이에 따른 적합한 사용 시나리오가 존재한다.

||Sync & Blocking|Async & Non-Blocking|
|---|:---:|:---:|
|설계|간단함|복잡함|
|유지보수|쉬움|어려움|
|성능|느림|빠름|

### Sync & Blocking

- 순차적인 의존성, 일관성(은행 시스템에서와 같은 데이터베이스 트랜잭션 등)이 필요한 시스템
    > 이는 작업의 결과가 서로 영향을 주는 경우를 말한다.
- 비교적 간단하고 적은 양의 작업을 처리하는 시스템
    > 편의성 도구나 CLI 기반 시스템 등이 이에 해당한다.

### Async & Non-Blocking

- 여러 작업을 동시에 처리할 수 있는 비동기 시스템
    > 웹 브라우저, 웹 크롤러 등에서 활용한다.
- 대용량 데이터나 많은 요청을 빠르게 처리하는 시스템
    > 웹 서버, 게임 서버 등 실시간 처리 시스템을 말한다.

### Node.js

Node.js 의 경우 두 방식을 적절히 선택하여 사용함으로써 성능과 효율성을 높인다.

- **Sync & Blocking**: 코드 실행 지연(`fs.readFileSync` 등)이나 순차적인 워크플로우
- **Async & Non-Blocking**: 이벤트 루프, 네트워크 요청 등 비동기 작업

이와 같은 구조 덕분에 단일 스레드에서도 높은 성능을 발휘할 수 있다.

## References

[my-growth-diary.log](https://velog.io/@maketheworldwise/SyncAsync-BlockingNon-Blocking-%EB%AC%B4%EC%8A%A8-%EC%B0%A8%EC%9D%B4%EC%9D%BC%EA%B9%8C#sync--blocking--async--blocking)<br>
[개발과 일상 사이](https://jh-7.tistory.com/25)<br>
[느리더라도 꾸준하게](https://steady-coding.tistory.com/531)<br>
[zxcev](https://velog.io/@mainfn/Blocking-Non-Blocking-Sync-Async-%EC%B0%A8%EC%9D%B4#sync-async)<br>
[Inpa Dev](https://inpa.tistory.com/entry/%F0%9F%91%A9%E2%80%8D%F0%9F%92%BB-%EB%8F%99%EA%B8%B0%EB%B9%84%EB%8F%99%EA%B8%B0-%EB%B8%94%EB%A1%9C%ED%82%B9%EB%85%BC%EB%B8%94%EB%A1%9C%ED%82%B9-%EA%B0%9C%EB%85%90-%EC%A0%95%EB%A6%AC#sync_blocking_%EC%A1%B0%ED%95%A9)
