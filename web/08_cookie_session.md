# 쿠키 
## 개념

- 서버가 사용자의 웹 브라우저에 전송하는 작은 데이터 조각
- 웹 브라우저 개발자가 웹 사이트에 접속한 클라이언트 확인하기 위해

## 등장 배경

- HTTP 통신은 stateless 하기 때문에 클라이언트를 확인하기 위해 쿠키라는 개념이 생김

## 사용

- 용도
    - 세션 관리
    - 개인 설정 유지
    - 사용자 트래킹 분석
    - 등..

## 특징

- 한개에 4KB까지 저장 가능 (텍스트파일 최대 300개 분량)
- 클라이언트에 저장됨
- 이름, 값, 만료날짜, 경로 정보가 있음
- (웹 브라우저 종료 || 만료일 도래) → 삭제됨
- 쿠키 정보 있으면 HTTP 요청시 헤어데 담아 보낸다
---
# 세션
## 개념

- 통신을 하기 위해 서로 연결된 순간부터 통신을 마칠 때까지의 기간
- 클라이언트가 웹서버에 연결된 순간 ~ (웹 브라우저 종료) HTTP 통신 끝난 순간
- 서버에 세션에 대한 정보를 저장해놓고, 세션 쿠키를 클라이언트에 줘서 서버가 클라이언트를 식별할 수 있게함

## 특징

- 따로 용량 제한이 없다 (서버 능력에 따라 다름)  - 서버에 세션 정보 저장하기 때문
- 서버에 세션 객체 생성하며, 각 클라이언트 마다 고유한 세션 ID 부여
- 쿠키를 사용하여 세션 ID 값을 클라이언트에게 response
- 웹 브라우저가 종료되면 세션 쿠키 삭제
- 클라이언트는 request header에 쿠키에 세션 ID 담아 보내고, 서버는 저장된 세션 정보와 확인

---
# 쿠키와 세션의 차이
## 쿠키

- 클라이언트에 정보 저장
- 주요 정보를 쿠키에 저장할 경우 누군가 마음만 먹으면 쿠키를 확인해 주요 정보를 볼 수 있음

## 세션

- 서버에 정보 저장
- 주요 정보는 서버에서 관리하고, 클라이언트는 쿠키에 세션 ID 만 가지고 있어 상대적으로 보안 강화
- 세션을 하용해도 쿠키에 저장된 세션 ID를 다른 사람이 가로채서 해당 ID로 변조해서 request를 보내면 보안에 허점이 생김
  - IP정보를 함꼐 사용하거나 쿠키 값 변조를 확인하는 방법 등으로 보완해서 사용 가능

## 결론

- 쿠키와 세션 모두 stateless, connectionless 한 HTTP통신에서 클라이언트를 식별하기 위해 쓰인다
- 주요 정보를 저장할 것인가 목적에 맞게 쿠키와 세션을 골라 사용하면 된다
- 다만, 주요한 정보는 세션 (서버에 저장)을 이용하자

---
# 쿠키에 보안 정보를 기록해도 되나요?
## 안된다!  (쿠키 보안 취약점)

- XSS(Cross Site Script) 공격
  - 자바 스크립트 이용하여 document.cookie 값을 탈취할 수 있음
  - 이를 막기 위해 쿠키에 HttpOnly옵션을 사용해 임의적인 script 접근을 막을 수는 있음
- sniffing
  - 네트워크를 통해 전송된느 쿠키값을 암호화 하지 않고 전송하는 경우 네트워크 스니핑 공격을 통해 쿠키 값 탈취 가능
- 공용 PC에서 쿠키값 유출
  - 영속성 쿠키는 하드디스크에 저장되며, 간단한 방법으로 접근 가능하기 때문


## 저장해도 되는 정보는?

- 암호화 된 정보
  - ex: JWT, MD5

## 결론

- 쿠키는 보안 취약점이 많으니 중요한 정보는 저장하지 말자

## 그럼 쿠키 말고 뭘 쓸까? : WebStorage

- 개념
  - 브라우저에 종속된, 클라이언트에 정보를 저장하는 K-V 형태의 데이터 저장소
- 종류
  - chrome, firefox, safari → sqlite에 저장
  - ie,opera → xml 데이터 파일형태로 저장
- 분류
  - localStroage
    - 로컬에 도메인 별로 지속되는 storage
    - 시간제한이 없고 브라우저가 꺼져도 죽지 않는다
    - 값을 지우려면 직접 지워줘야 한다
  - sessionStorage
    - 세션 종료시 데이터가 지워진다
    - 이 때 세션이란 새 탭이 만들어 졌을 때~ 탭을 종료했을 때
- 쿠키와의 차이점
  - 장점 (비교 우위)
    - WebStorage는 시간제한과 갯수제한은 없다. 하지만 용량제한은 있다
    - WebStorage는 자바스크립트 객체. 따라서 web storage 안에 자바 스크립트 객체를 넣는것도 가능
    - request할 때 쿠키는 모든 값을 header에 넣어 보내야 했는데 webStroage는 개발자가 선별해서 넘겨도 됨 → HTTP 통신 부하 감소
    - 쿠키는 자신의 변화를 감지할 방법이 없지만, WebStroage는 이벤트로 감지 가능
  - 단점
    - 쿠키보다 WebStorage쓰는 방법이 더 까다롭다
    - 데이터 영속성을 띄는 localStorage는 일일이 데이터 지워줘야 하며, HTTP 통신시 항상 코드를 작성해 데이터 선별해 넘겨줘야하기 때문에 유지보수가 더 까다로움
- 세션과의 차이점
  - 세션은 서버에 데이터 저장, WebStorage는 클라이언트에 정보 저장
  - WebStorage는 쿠키를 보완한게 맞지만, 여전히 클라이언트에 저장한다는 점에서 세션보다 보안 이슈 발생 가능성이 높음
  - 다만 세션은 서버에 부하를 많이 걸리게 할 수 있다는 점에서 WebStorage를 더 활용하기도 함