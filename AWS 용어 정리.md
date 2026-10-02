s3 전송가속 : 클라이언트와 s3 사이의 업로드/다운로드 속도 향상 -> 보통 멀티파트 업로드와 같이 사용

s3 크로스 리전 복제 : 비동기 복제여서 지연이 높음

AWS snowball edge : 운영부담과 지연이 큼

Amazon EC2 인스턴스 : 가상서버

Amazon EBS : EC2에 저장공간을 더해줌

Amazon Redshift : 대량의 데이터를 모아두고 분석용 SQL 쿼리를 빠르게 돌림

Amazon CloudWatch : aws의 리소스와 애플리케이션을 모니터링하는 서비스

Amazon Athena : 저장된 데이터를 SQL로 바로 조회하는 서비스 / 서버리스 방식

AWS Glue : 흩어져있는 데이터를 추출 -> 변환 -> 적재해서 분석형태로 만들어줌

Amazon EMR : 하둡/스파크 같은 빅데이터 처리 프레임워크를 AWS에서 실행

aws:PrincipalOrgID : 조직 내 모든 계정 

aws:PrincipalOrgPaths : 조직 내 특정 OU(부서별)

vpc : 내 전용 네트워크 공간

게이트웨이 vpc 엔드포인트 : vpc 안의 서버가 인터넷을 거치지않고 S3나 db에 바로 접근하게 해줌

amazon api gateway : api를 만들고, 배포하고, 관리해주는 완전관리형 서비스

로드 밸런서 : 들어오는 트래픽을 여러 대상에 골고루 나눠주는 서비스, 서버 한대에 요청이 몰리는 것을 막고 
		 서버가 죽어도 서비스가 계속되게 해준다

amazon EFS : 여러 EC2 인스턴스가 동시에 공유해서 쓸 수 있는 파일 스토리지 