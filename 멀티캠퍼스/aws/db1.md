#### MYSQL/Aurora DB



데이터베이스 마스터/슬레이브 형식으로 만들기.

아키텍처는 Bastion 호스트는 퍼블릭 서브넷, Aurora DB는 프라이빗 서브넷에 위치함

보안그룹 설정은 호스트는 ssh(22번) 포트 허용, DB는 3306 포트 허용

라우팅 설정은 퍼블릭 라우트는 기본 게이트웨이 설정,  프라이빗 라우트는 VPC 내부만 설정



#### DB 생성

DB 인스턴스 클래스 크기는 t2.small, dev/test 모드, 보안그룹 default는 제외하고 Database 추가, 최초 데이터베이스 이름과 관리자 이름 및 암호 설정



#### MYSQL Workbench

standard TCP/IP over SSH 방식으로 Bastion 호스트에 접속하여 3306 포트로 접속하는 방식



