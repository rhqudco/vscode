## 서버 구현 패턴

### 모델2 방식 (MVC 패턴)
## 사진

### FrontController 패턴
- 모든 클라이언트 요청을 한 곳에서 처리하도록 하나의 대표 컨트롤러 사용
- 별도의 클래스를 추가하지 않고 FrontController가 다 처리 
  - (FrontController 내용이 길고 복잡해짐)
- 클라이언트의 요청을 한 곳으로 집중시켜서 효율적으로 개발 및 유지보수 가능
## 사진

### Command 패턴
- FrontController가 모든 클라이언트 요청을 직접 처리하지 않고 해당 클래스가 처리
- FrontController가 수행하던 작업을 각 클래스로 분산 처리
- 각 클래스는 통일된 형식(규격)으로 처리하도록 interface로 구현
## 사진


### Spring MVC 구조
## 사진