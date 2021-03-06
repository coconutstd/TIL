# AWS 정리
## IAM
처음 aws를 사용할때 보통 루트 계정으로 연습 겸 테스트용으로 사용합니다. 하지만 실제 서비스 운영시에는 , 네트워크를 구축한 상태에서 EC2, S3, RDS 등
다양한 리소스를 개발자 유형 별로 접근 제어를 시킬 필요가 있는데 이럴 때 IAM을 사용합니다.

IAM을 사용할 때에는 **역할(Role), 정책(Policy)**를 올바르게 구성하여 IAM사용자와 연결하는게 중요합니다. 간단히 얘기해서 역할은 여러 정책들을 포함시킴으로써 정의됩니다. 또한, 정책에는 aws 사용자 편의를 위해 크게 두가지 방식이 존재합니다.

- 관리형 정책(Managed Policy) :  재사용을 위해 여러 정책을 그룹지어 관리할 수 있으며, 역할에서 관리형 정책을 삭제시 해당 정책들 또한 모두 제외됩니다.
- 인라인 정책(Inline Policy): 재사용을 염두해 두지 않고, 원하는 정책을 바로 연결할 수 있습니다.



## EC2

EC2는 풀어서 쓰면 ECC(Elastic Compute Cloud)의 약자입니다. 말그래도 가상의 컴퓨터를 이야기 합니다. 서버를 빌리고자 할 때는 디폴트로 온디맨드 형식으로 빌릴수 있으며, 가장 기본적인 t2.micro 사이즈의 컴퓨터를 선택하여 시간당 16원 정도 부과됩니다. EC2를 빌리고자 할 때는 다음 몇가지를 신경쓰면 됩니다.

- AMI(Amazon Machine Image) - 아마존에서 제작한 기본 운영체제 이미지 -> 가상 이미지에 여러 프로그램을 설치하여 커스텀 이미지로 만들수도 있음
- 인스턴스 유형 - 기본은 t2.micro이나 EC2 요금표를 보고 적절히 선택, 간혹 1GB의 적은 메모리로 인해 프로그램 빌드시 느릴 수 있음
- 인스턴스 세부정보
  - VPC : 우리가 VPC를 굳이 만들지 않아도 각 리전마다 기본 VPC 및 서브넷이 설정되어 있음
  - 퍼블릭 IP 자동 할당: 외부에서 접근할 수 있는 IP를 할당해줍니다.
- 스토리지(기본) , 태그 (대시보드에서 편하게 보기위해 Name을 키, 원하는 이름을 값으로 설정)
- 보안그룹은 NACL과는 다른 AWS 리소스에 사용되며, 상태 저장 방화벽인 것이 특징입니다.(인바운드 규칙 설정시 자동으로 아웃바운드도 같게 설정)
  - 보통 터미널 접속을 위한 ssh와 웹 접속을 위한 http, https 가 많이 사용되며 서버에 깔리는 애플리케이션에 따라 추가할 수 있습니다.
  - 다만 모든 포트를 개방한 후 특정 포트만 차단하는 블랙리스트 방식보다는 모든 포트를 차단 후 특정 포트만 열어두는 화이트리스트 방식이 안전하다
- 마지막으로 검토시작 버튼을 누르면 우리가 빌린 EC2에 접속할 수 있는 키페어 쌍을 다운받을 수 있다, 한 번 잃어버리면 다시 발급이 불가하니 유의할것