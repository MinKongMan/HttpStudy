
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
- https://www.google.com:443/search?q=hello&hl=ko


### URN
- Name : 리소스에 이름을 부여
