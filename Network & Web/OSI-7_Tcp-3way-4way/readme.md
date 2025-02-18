# 질문들 리스트

## OSI 7계층

#### 1. OSI 7계층을 간단하게 설명하고 해당하는 장비를 간단하게 말해주세요

1) 물리 계층: 디지털 데이터를 전기적 신호로 변환해 입출력을 담당한다. 전송하는데 필요한 기능을 제공. 허브, 통신케이블, 리피터  
2) 데이터 링크 계층: 물리계층의 데이터를 신뢰할 수 있는 링크로 변환한다. 물리적 주소인 MAC address로 통신한다. 브릿지, L2 스위치  
3) 네트워크 계층: 논리적 주소인 IP 주소룰 기반으로 패킷의 전송 경로를 결정한다. 라우팅  
4) 전송 계층: TCP/UDP 포트 정보를 참조해 데이터 전송  
5) 세션 계층: 통신 시스템 사용자 간의 연결을 유지 및 설정  
6) 표현 계층: 세션 계층 간 주고받는 인터페이스 일관성있게 제공  
7) 응용 계층: 사용자가 네트워크에 접근할 수 있는 서비스 제공

#### 2. ARP와 RARP 비교

공통점은 둘다 네트워크 계층에서 사용되는 주소 결정 프로토콜  
ARP는 IP주소에서 MAC 주소를 알아내고  
RARP는 MAC주소에서 IP 주소를 알아낸다.

#### 3. 브릿지와 스위치 비교

공통점은 둘다 데이터 링크 계층에서 전송 거리를 연장하는 장치  
브릿지는 소프트웨어적으로 프레임을 다시 만들고 전송해 느림  
스위치는 성능에 따라 L2,L3,L4,L7으로 구분되며 하드웨어적으로 처리해 더 빠름

#### 4.허브와 리피터 비교

공통점은 물리계층에서 전기적 신호를 증폭시켜 전송 거리를 연장하는 장치로 네트워크 신호가 연결된 모든 PC에 전달되기 때문에 연결된 장치가 많을 수록 부하가 심해짐  
허브는 패킷 모니터링과 멀티 포트를 지원해 문제가 생긴 곳을 고립할 수 있다.

#### 5. MAC은 뭐에요?

Media Access Control는 네트워크 통신을 위한 물리적 주소로 사용되며 기기를 고유적으로 식별하게 해주는 역할을 합니다.

## TCP

#### 1. 3-Way Handshaking과 4-Way Handshaking는 언제 쓰이나요?

3WH는 세션을 초기화할 때. 4WH는 세션을 종료할 때 쓰인다.

#### 2. 3-Way Handshaking의 과정

클라이언트가 서버에 접속을 요청하는 SYN 패킷 전송하고 클라이언트는 SYN/ACK 응답을 기다리는 SYN\_SENT 상태로 기다림  
서버는 SYN 요청을 받고 클라이언트에게 요청을 수락하는 SYN/ACK flag가 설정된 패킷을 전송하고 클라이언트가 ACK를 응답하기 기다리는 SYN\_RECEIVED 상태로 기다림  
클라이언트는 서버에게 ACK를 보내면 서버는 Established 상태가 되고  
이후 부터는 연결이 이루어 진다.

#### 3. 클라이언트가 서버에 보낸 SYN/ACK 요청을 받지 못하는 경우 어떻게 되는가?

클라이언트는 서버에 SYN 요청을 보내고 시간을 잰다. timeout이 발생하기 전까지 SYN/ACK 응답이 오지않으면 다신 SYN를 보내고 응답을 기다린다.

#### 4. 3-Way Handshaking을 사용하는 이유는?

양쪽 모두 데이터를 전송할 준비가 된 것을 보장한다.  
응용 프로그램이 데이터를 전송하기 전에 먼저 정확한 전송을 보장하기 위해 사전에 세션을 수립하는 과정이다.

#### 5. 4-Way Handshaking의 과정

클라이언트가 연결을 종료하겠다는 FIN flag 전송  
서버는 일단 확인 했다는 ACK 응답을 보내고 자신의 통신이 끝날 때까지 TIME\_WAIT 상태로 기다림.  
서버가 통신이 끝났으면 연결이 종료되었다고 클라이언트에게 FIN flag를 전송  
클라이언트는 확인 ACK 응답을 전송한다.

#### 6. 서버가 마지막에 FIN flag를 전송하는 이유는?

서버가 아직 클라이언트에게 보낼 데이터가 남아있는 경우 데이터를 다 전송하지 못한채 클라이언트가 포트를 닫아버리게 되므로 서버도 종료될 준비가 되었다는 의미로 FIN flag를 전송한다.

#### 7. 마지막에 클라이언트가 굳이 ACK를 보내는 이유는?

서버가 보낸 FIN flag를 클라이언트가 받지 못하면 계속 종료되지 못한 채로 기다려야한다. 하지만 서버는 이미 포트를 닫고 응답하지 않는 상태이기 때문에 클라이언트가 불필요한 자원 소모를 막기위해 확인 패킷을 보내는 것이다.

#### 8. HTTPS 환경에서의 3-Way HandShaking 과정

클라이언트는 서버에 SSL 정보 및 암호화 방식, 무작위 바이트 문자열 A를 전송한다.  
서버는 클라이언트에게 인증서, 무작위 바이트 문자열 B를 전송한다.  
클라이언트가 CA에 인증서 목록이 있는지 확인 후 공개 키를 받는다.  
클라이언트는 서버에게 무작위 바이트 문자열 A와 B를 조합하고 공개키로 암호화하여 전송한다.  
서버에서는 비밀키로 받은 무작위 바이트 문자열 조합을 복호화하고 이것으로 세션키를 만들어 해당 세션키를 가지고 암호화한 데이터를 주고 받는다.

#### 9. TCP와 UDP의 차이는 무엇인가요 ?

TCP는 신뢰성 기반 연결 지향 프로토콜인 반면 UDP는 신뢰성 없는 비연결 지향 프로토콜입니다. TCP는 연결 된 이후 3WayHandShake를 통해 데이터를 신뢰성을 보장하며 주고 받는 반면 UDP는 데이터 손실을 신경쓰지 않고 전송하는 차이점이 있습니다.


참고: [네트워크 면접 예상 질문](https://hyonee.tistory.com/136)
