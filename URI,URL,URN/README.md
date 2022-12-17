# URI, URL, URN
### URI
- Uniform : 리소스를 식별하는 통일된 방식
- Resource : 자원, URI로 식별할 수 있는 모든 것(제한 없음)
- Identifier : 다른 항목과 구분하는데 필요한 정보

### URL
- Locator : 리소스가 있는 위치 지정
- scheme : //[userinfo@]host[:port][/path][?query][#fragment]
> scheme
> > 주로 프로토콜이 사용됨(어떤 방식으로 작동될 것인가에 대한 Client와 Server간의 규칙)<br/>
> > ex) http, https, ftp 등등<br/>
> > http는 80퐅, https는 443포트를 주로 사용(포트는 생략 가능)<br/>
> > https = http+보안 추가(Http Secure)<br/>

> userinfo
> > URL에 사용자 정보를 포함해서 인증할 때 사용 (거의 사용하지 않음)

> host
> > 도메인명 또는 IP 주소를 직접 사용 가능

> port
> > 접속 포트, 일반적으로 생략, 생략 시 http는 80, https는 443

> path
> > 리소스가 있는 경로, 계층적 구조 <br/>

> query
> > key, value의 형태<br/>
> > ?로 시작, &로 추가 가능

> fragment
> > html 내부 북마크 등에 사용

##### https://www.google.com:443/search?q=hello&hl=ko 검색 시
1. DNS 조회 (www.google.com:443)
2. HTTP 요청 메시지 생성
> GET /search?q=hello&hl=ko HTTP/1.1 HOST:www.google.com 이런 모양
> HTTP메소드/ path정보/ HTTP 버전 정보/ HOST 정보
3. 메시지 생성 후 SOCKET 라이브러리를 통해 TCP/IP로 전달
4. TCP/IP에서 받은 메시지에 패킷 생성
5. 인터넷 망으로 전달
6. 망을 통해 구글 서버로 전달 후 구글 서버는 HTTP 요청 메시지 해독 후 HTTP 응답 메시지 생성
7. 구글 서버 또한 TCP/IP 패킷 생성 후 응답 메시지를 담고 인터넷 망으로 전달
8. Client는 패킷에 들어있는 응답메시지를 해독 후 화면으로 전달


### URN
- Name : 리소스에 이름을 부여
