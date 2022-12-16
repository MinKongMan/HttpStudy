
# IP vs TCP,UDP
### IP - 복잡한 인터넷 망에서 메세지를 보내기 위한 수단
- IP 패킷 정보
> 20 ~ 60 bytes의 Header(Source IP, Destination IP 32bit씩 포함 등) + Data -> 총 20~65535 bytes
- 비연결성 : 패킷을 보낼 때 받는 쪽이 받을 수 있는 상태인지 알 수 없음<br/>
- 비신뢰성 
> 패킷이 소실되어도 알 수 없음 -> 서버에 문제가 생겨 패킷이 전송되는 중 소실되는 현상<br/>
> 패킷 전달 순서 문제 발생 -> 패킷들이 중간에 다른 노드를 탈 수 있어 받는 입장에서 순서가 엉망이 될 수 있다.<br/>

### TCP
- TCP/IP 패킷 정보
> IP 패킷 내부에 TCP 세그먼트가 있음
> > 출발지 PORT, 목적지 PORT, 전송 제어, 순서 등과 같은 정보가 있어 IP에서의 한계가 드러나지 않음
- 연결 지향 - 3 way handshake -> IP의 비연결성 해결
> 1. Client가 SYNC(연결 요청)를 Server에게 보냄
> 2. Server가 SYNC(연결 요청) + ACK(연결 확인)를 Client에게 보냄
> 3. Client가 Server에게 ACK(연결 확인)를 보냄(연결 완료)
- 데이터 전달 보증 -> IP의 비신뢰성 해결
> Client가 Server에 데이터를 전송하면 Server는 받았다고 Client에게 알려줌 (전달 보증)
- 순서 보장 -> IP의 비신뢰성 해결<br/>
> Client가 패킷1, 2, 3 순서로 보냄 -> Server는 1, 3, 2순서로 받음
> 그럼 Server에서 3 2를 버리고 2번부터 다시 보내라고 Client에게 메세지를 보냄 

### UDP
- IP의 특징과 거의 유사
> 비연결성
> 데이터 전달보증 X
> 순서 보증 X
- 다만 PORT가 추가됨
> PORT를 통해 하나의 IP에서 사용하는 여러 Application이 받는 패킷을 구분하도록 해줌
> 같은 IP 내에서 프로세스 구분
- TCP는 이미 정해진 규칙이 있기 때문에 개발자가 UDP를 사용하며 어플리케이션 단에서 수정하면 됨


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

# Http
- 기반 프로토콜
> TCP : HTTP/1.1 ,  HTTP/2
> UDP : HTTP/3
- TCP가 안정적이긴 하나 UDP가 속도가 빠르고, 어플리케이션 단에서 최적화 함으로 UDP를 쓰는 추세다.
- 클라이언트 서버 구조
- 무상태 프로토콜(stateless)
- HTTP 메시지
### Http 메서드
- GET : 리소스 조회
> 서버에 전달하고 싶은 데이터는 query를 통해 전달<br/>
> 메시지 바디를 사용해서 데이터를 전달할 순 있지만, 지원하지 않는 곳이 많아 권장하지 않음<br/>
- POST : 요청 데이터 처리, 주로 등록에 사용
> 메시지 바디를 통해 서버로 요청 데이터 전달 -> 서버는 요청 데이터를 처리<br/>
- PUT : 리소스를 대체, 해당 리소스가 없으면 생성
> 리소스를 완전히 대체한다
> > 기존 필드에 "age" : 20, "username":"kang" 이라는 값이 있고 <br/>
> > "age":50 을 전송하면 username은 사라지고 "age":50으로 바뀜 <br/>
> 클라이언트가 리소스 위치를 알고 URI 지정(POST와 차이점)
- PATCH : 리소스 부분 변경
> PUT에서 완전히 대체되는 성질을 부분 변경으로 바뀜
- DELETE : 리소스 삭제
### Http 메서드의 속성
- 안전 : 호출해도 리소스를 변경하지 않는다.
- 멱등 : 몇 번을 호출하든 결과가 똑같음. (외부 요인으로 중간에 리소스가 변경된 것은 고려하지 않음)
> GET : 여러번 호출을 해도 같은 결과가 조회된다.<br/>
> PUT : 똑같은 파일을 업로드해도 결과가 같다.<br/>
> DELETE : 결과를 삭제. 같은 요청을 여러번 해도 삭제된 결과는 똑같다.<br/>
> POST : 멱등 아님 -> 두 번 호출하면 같은 결제가 중복해서 발생할 수 있음. <br/>
> 활용 : 자동 복구 메커니즘 (서버가 Time Out 등으로 정상 응답을 못 주었을 때 <br/>
- 캐시 가능
