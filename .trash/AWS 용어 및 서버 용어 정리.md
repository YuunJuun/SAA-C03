# IAM
AWS 사용자와 서비스 권한을 관리하는 기능
- 이 사용자가 EC2를 생성할 수 있는가?
- EC2 서버가 S3 파일을 읽을 수 있는가?
- EKS가 ECR 이미지를 가져올 수 있는가?

User: 실제 사용자 계정
Role: AWS 서비스나 애플리케이션이 임시로 사용하는 권한
Policy: 허용하거나 거부할 작업을 적어 놓은 권한 문서

# VPC
AWS 안에 만드는 나만의 가상 네트워크

- CIDR - 네트워크가 사용할 IP 주소 범위
- Subnet - VPC 네트워크를 더 작은 네트워크를 나눈 것
- Public Subnet - 인터넷에서 직접 접근할 수 있도록 구성한 서브넷
- Private Subnet - 인터넷에서 직접 접근하지 못하도록 만든 서브넷
- Internet Gateway - VPC가 인터넷과 통신할 수 있도록 연결하는 출입구

# Helm

1. Chart = 하나의 배포 패키지
- YAML 여러 개를 하나의 디렉토리로 묶고, 그 안의 값들을 변수로 바꿔놓은 것 

2. Release = chart를 실제로 클러스터에 "설치한 인스턴스"
- 같은 chart를 이름만 다르게 여러 번 설치할 수 있다.
- chart를 붕어빵 틀이라고 생각하면 release 는 chart로 구운 붕어빵 하나 
	같은 틀로 이름이 다른 릴리즈를 여러개 생성 가능
	
3. values.yaml = chart에 넘기는 "설정값"
- 같은 chart라도 values 값만 바꾸면 dev/release/prod 환경별로 다르게 배포 가능
- mychart/values.yaml (chart 기본 값)
  values-prod.yaml (기본 값에 덮어 쓸 prod 값)

4. Repository = chart 들을 모아둔 저장소
- 깃헙 레포가 아니라, helm repo add 로 등록하는 chart 전용 저장소

** 정리 **
현재 파일 구조는 각각의 yaml 파일들이 다 각자의 값을 가지고있다.
예를 들어 prod/deploy_https_qKet_frontend.yaml 의 replicas의 값을 수정해야한다고 하자
그러면 prod 경로에 있는 replicas 값을 가지고 있는 yaml 파일들을 일일이 들어가서 수정해야한다.
하지만 helm 사용하여 values.yaml (기본 설정값)을 만들어놨다고하면 여기에서 그냥 prod 설정값만
수정해야되는 값으로만 바꿔주면 된다. 

한마디로 말하면 문제가 생겼을 때 고칠 곳이 여러 yaml 파일 전체에서 그 값이 정의된 values.yaml 이 파일
한 곳으로 줄어든다.

