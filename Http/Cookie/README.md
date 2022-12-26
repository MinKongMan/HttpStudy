# Cookie

- Set-Cookie : 서버에서 클라이언트로 쿠키 전달(응답)



- Cookie : 클라이언트가 서버에서 받은 쿠키를 저장하고, HTTP 요청시 서버로 전달

```
쿠키 미사용
1) 어떤 페이지에 접속 후 로그인 정보를 Post로 서버로 보냄
2) 서버에서 200OK 내림(로그인된 html 나옴)
3) 다시 그 페이지에 접근을 할 때(GET 방식) 서버는 1)인 사람인지 모르고 손님으로 판단하고 200OK 내림
3-1) http 특성 -> 전송 다 되면 연결 끊어버림

대안 -> 모든 요청에 사용자 정보 포함해서 보냄.
      하지만 보안에 문제점이 많다.
      
      
      
쿠키 사용
1) 어떤 페이지 접속 후 로그인 정보를 Post로 서버로 보냄
2) 서버는 200OK를 내릴 때 Set-Cookie: user=사용자 정보 라는 헤더를 만들어서 응답함
3) 웹 브라우저는 웹 브라우저 내부에 쿠키 저장소에 user=사용자 정보를 저장한다.
4) 다시 1)의 페이지에 접속할 때 쿠키를 무조건 꺼내서 http 헤더를 만들고 서버에 request 메세지를 보냄
5) 서버는 쿠키 헤더의 정보를 바탕으로 정보 파악


※ 모든 곳에 쿠키 정보를 보내면 보안에 문제가 생기므로 제약하는 방법이 있다.
예) set-cookie: sessionId=XX; expire=Sat, 24, Dec-2022 00:00:00 GMT; path=/; domain=.google.com;Secure
sessionId가 XX

expire : 기간 (생명 주기 관리)
      세션 쿠키 : 만료 날짜를 생략하면 브라우저가 종료될 때까지만 유지
      영속 쿠키 : 만료 날짜를 입력하면 해당 날짜까지 유지
path : ~한 경로들에 대해 허용
      ex) path = /home -> 이 경로를 포함한 하위 경로 페이지만 쿠키 접근
      일반적으로 path = /루트로 지정

domain : ~한 도메인에 대해 허용
      명시 : 명시한 문서 기준 도메인 + 서브 도메인 포함
            ex) domain = example.org -> example.org는 물론이고 dev.example.org도 쿠키 접근
      생략 : 현재 문서 기준 도메인만 적용
            ex) example.org에서 쿠키 생성하고 domain 지정을 생략 -> example.org 이외에 쿠키 미접근
Secure : 보안 정보를 넣음
      1) Secure : 쿠키는 http https를 구분하지 않고 전송하지만 Secure를 적용하면 https인 경우에만 전송
      2) HttpOnly : XSS 공격 방지, 자바스크립트에서 접근 불가, Http 전송에만 사용
      3) SameSite : XSRF 공격 방지, 요청 도메인과 쿠키에 설정된 도메인이 같은 경우에만 쿠키 전송
사용처 : 1) 사용자 로그인 세션 관리
        2) 광고 정보 트래킹
        
- 쿠키 정보는 항상 서버에 전송되므로 네트워크 트래픽 추가 유발이 발생
      -> 최소한의 정보만 사용하면서 예방(세션id, 인증 토큰)
- 민감한 정보는 저장하면 안됨 (주민번호, 신용카드 정보)





```

