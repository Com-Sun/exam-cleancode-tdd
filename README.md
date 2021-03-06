# 개요

## ParkingLotParkingService

- 주차에 관한 기능을 제공한다

## ParkingLotPaymentService

- 결제에 관한 기능을 제공한다
- PaycoServer, ParkingFee, ParkingLotRepository에 의존한다.

## ParkingLotRepository

- carParkedTimeInfo: 주차된 차의 시간정보를 관리하는 Map<Car, LocalDateTime>타입 속성
- carParkedSpaceInfe: 주차된 차의 공간정보를 관리하는 Map<Car, String>타입 속성
- parkingSpace: 주차 공간이 사용 가능한지를 관리하는 Map<String, Boolean>타입 속성

---

- 주차된 차의 모든 정보를 관리한다.


# 기능 구현

## Spec 1

### 주차장에 차가 들어온다.
  - 번호판을 Scan하여 ParkingLotRepository에 저장하는 기능 구현
### A-1에 주차한다.
  - 만약 A-1이 사용중이라면 Throw Exception 기능 구현
  - 아니라면 A-1을 사용중인 상태로 만드는 기능 구현
### 주차장에서 차가 나간다.
  - 주차한 시간만큼 요금표에 따른 fee 청구 기능 구현
  - User가 돈이 없을 시 Throw Exception 기능 구현 (나갈 수 없음)
  - 사용중이던 주차공간을 사용할 수 있는상태로 변경 기능 구현

## Spec 2

scan() / chargeParkingFeeToUser() 메서드가 동시에 입구 / 출구 갯수보다 많이 실행될 수 없음.

### 주차장 입구가 3개입니다.

- ParkingLotParkingService에서 Scan메서드가 동시에 4번 이상 발생시 Throw CarCannotEnterOverEntranceNumber 기능 구현

### 주차장 출구가 3개입니다.
- `TODO: ParkingLotPaymentService에서 요금계산 메서드가 동시에 4번 이상 발생시 Throw Exception`


## Spec 3

### 주차장 요금표 변경 기능 구현
- ParkingFee 속성을 통해 평소엔 WEEKDAY 요금 적용
- WEEKEND 요금 적용시 다른 요금표 적용
- 경차는 50% 할인 기능 구현
- 트럭 타입 Car객체가 처음 Scan 될 시 Throw Exception 기능 구현 (트럭 주차 불가)


## Spec4

### 사용자가 Payco 회원일 경우 주차요금이 10% 할인

- Payco 서버는 Mocking
- 회원 인증 성공시 주차요금 10% 할인기능 구현
- Payco 인증이 안될 경우, 할인 적용 없이 요금 청구 기능 구현

### 시간주차권 존재

- `TODO: 주차권 기능 구현`
