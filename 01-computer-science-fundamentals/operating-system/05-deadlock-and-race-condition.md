# 데드락과 레이스 컨디션

## 교착 상태 (데드락, Deadlock)

### 정의
- 둘 이상의 프로세스(또는 스레드)가  
  **서로 상대방이 가진 자원을 기다리면서**
  **영원히 진행하지 못하는 상태**

- 이 상태에서는 프로세스가 **Blocked State(대기 상태)**에 머무르게 되며,  
  시스템이 멈추거나 비정상적으로 동작할 수 있다.

<br>

<img src="img/deadlock.png" alt="데드락 Deadlock" width="500">

### 예시 상황

- **Thread 1** → Resource 2를 가지고 있음  
- **Thread 2** → Resource 1을 가지고 있음  

#### 그런데...

- Thread 1은 **Resource 1**이 필요해서 요청함  
- Thread 2는 **Resource 2**가 필요해서 요청함  

#### 하지만

- Thread 1은 Resource 2를 놓지 않음  
- Thread 2는 Resource 1을 놓지 않음  

### 결과
- 서로가 서로를 기다리며 아무도 자원을 양보하지 않음으로 둘다 영원히 멈춤 (Blocked State)

<br><br>

## 경쟁 상태 (레이스 컨디션, Race Condition)

### 정의
- 둘 이상의 스레드 또는 프로세스가  
  **공유 자원(변수, 메모리 등)** 에 동시에 접근하여 수정할 때 발생하는 문제
- 실행 순서에 따라 결과가 달라지며,  
  **예상하지 못한 값**이 저장될 수 있음

<img src="img/race_condition.png" alt="레이스컨디션 Race Condition" width="500">

### 예시 상황

#### 상황 가정

- 하나의 공유 변수 `count = 0`
- 두 개의 스레드가 동시에 `count++` 실행

#### 실행 과정 (문제 발생)

1. Thread A가 `count` 값을 읽음 → 0
2. Thread B도 `count` 값을 읽음 → 0
3. Thread A가 `count + 1` 계산 → 1
4. Thread B도 `count + 1` 계산 → 1
5. Thread A가 1 저장
6. Thread B도 1 저장

- 최종 결과: `count = 1`  
- 하지만 기대 결과는 `2`

### 핵심 특징

1. 공유 자원이 존재함
2. 동시에 접근함
3. 실행 순서에 따라 결과가 달라짐
4. 비결정적인 결과가 발생함



<br><br>

## 참고자료
- https://hmk1022.tistory.com/entry/%EA%B2%BD%EC%9F%81%EC%83%81%ED%83%9CRace-Condition%EC%99%80-%EB%8D%B0%EB%93%9C%EB%9D%BD#:~:text=%EB%94%B0%EB%9D%BC%EC%84%9C%2C%20JavaScript%EC%97%90%EC%84%9C%EB%8F%84%20%EB%A9%80%ED%8B%B0%EC%8A%A4%EB%A0%88%EB%93%9C%EB%A5%BC%20%EC%82%AC%EC%9A%A9%ED%95%A0%20%EB%95%8C%EB%8A%94%2C%20%EC%A0%81%EC%A0%88%ED%95%9C%20%EB%8F%99%EA%B8%B0%ED%99%94,%EB%8C%80%ED%95%9C%20%EC%A0%91%EA%B7%BC%EC%9D%84%20%EA%B4%80%EB%A6%AC%ED%95%98%EA%B3%A0%2C%20%EA%B2%BD%EC%9F%81%20%EC%83%81%ED%83%9C%EB%82%98%20%EB%8D%B0%EB%93%9C%EB%9D%BD%EA%B3%BC%20%EA%B0%99%EC%9D%80