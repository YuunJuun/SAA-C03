MyBatis_강좌정리

///////////////////////
라이브러리(library)?
- * .jar서(ex. * .js)의미로서 외부에서 만들어진 클래스파일들의 묶음으로
  다운로드 받아서 build path에서 사용.

프레임워크(framework)?
-  * .jar + 프로그램 개발하기 위한 틀

///////////////////////
MyBatis 프레임워크(framework)

1. 개요
  - JDBC 사용을 편리하고 효율적으로 기능이 추가된 형태의 SQL Mapping Framework임.
    ( 개발자가 메서드 호출하면, 이 메서드에 해당하는 sql문을 자동으로 실행해줌 )
  - ibatis ( 초창기 버전명 )

2. 환경설정

  - mybatis jar 필요
    http://mybatis.org 에서 다운로드 받음  (mybatis-3.5.17.jar)

  - mysql 드라이버 필요

  위 2개의 jar파일을 (mybatis-3.5.17.jar, mysql-connector-j-8.0.33.jar) eclipse에서 build path해야됨.


3. MyBatis 사용방법


	1) jdbc에서 사용했던 4가지정보를 외부파일에 저장함.

     String driver = "com.mysql.cj.jdbc.Driver"; // 핵심이 되는 클래스명
     String url = "jdbc:mysql://localhost:3306/testdb";
     String userid ="root";
     String passwd = "1234";

    ==> 파일명.properties 
	==> 저장방법
		src
			com
				config
					jdbc.properties
	==> 현재 eclipse 에서 사용중인 인코딩은 기본적으로 utf-8 임
		생성된 jdbc.properties 파일도 utf-8로 인코딩을 변경하자
	```
# 주석문
# key=value
jdbc.driver=com.mysql.cj.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/testdb
jdbc.userid=root
jdbc.passwd=1234
	```

	2)  DTO 클래스 작성
	-  MyBatis 에서 필수
		==> DTO에 저장된 데이터
	- 일반적으로 테이블당 한개씩 작성
		ex. dept 테이블용 DeptDTO.java
		emp 테이블영 EmpDTO.java
		
	- DTO 클래스의 변수명은 테이블의 컬럼명과 일치시켜주는 것을 권장함

		ex. dept 테이블 ---------------------> com.dto.DeptDTO.java
			컬럼
			dept ------------------------- > int deptno;
			dname ------------------------ > String dname;
			loc ---------------------------- > String loc;
			sal --------------------------- > int slalary;

	- DTO 클래스에서 기본생성자와 getter/setter 메서드는 필수임

		==> DTO에 저장된 데이터는 자동으로 MyBatis 에서 가져와서 SQL 문에 사용됨
		반대로 SQL문 실행된 결과를 자동으로 DTO에 저장시킨다

	3) 2개의 xml 파일이 필요
	- * .xml
		/////////////////////////////////////////////////////
		xml (eXtensible Markup Language: 확장가능한 마크업 언어) ex. HTML
		가. 태그로 구성
			ex. <시작태그>
				컨텐츠 <== 태그 또는 문자열
			 <종료태그>

		나. 시작태그에는 속성(key=value)을 가질 수 있음
			ex. <태그 key=value  key=value>

		다. 반드시 여러 태그들을 포함하는 단하나의 root태그를 가져야 된다.

		ex. 
			<태그>
			<태그></태그>
			<태그></태그>
			.....
			</태그>

		라. 컨텐츠가 없는 태그를 빈태그(empty)가 가능
			ex. <시작태그></종료태그>
			  <시작태그/>

		HTML
		- 태그명과 속성명등이 정해져 있음
		- 용도는 웹페이지의 구조를 만들때 사용 
		
		xml (확장가능한 마크업 언어)
		- 태그명과 속성명등을 마음대로 지정 가능
			ex.
		```html
<person>
	<name>홍길동</name>
	<age>20</age>
<person>
		```
		- 용도는 서로 다른 플랫폼에서의 데이터 전달용(공통포맷)

			만약 A에서 다음과 같이 xml만들었다고 가정.
		```html
    <person>
        <name>홍길동</name>
		<age>20</age>
		<adderess post="1234" city="seoul" />
	</person>
		```

		B에서는 프로그램적으로 xml를 읽는 작업이 필요함.
	     1)루트태그명은 person
	     2)첫번째 자식명은 name
	     3)마지막 자식명은 age
		 
	- A와 B간의 xml만들때 규칙(태그명,순서,속성명,타입등)을 정해서 문서화 했음.
	  문서화하는 방법
	   가. dtd 방법
		- * .dtd

	   나. schema 방법
	    - * .xsd

 /////////////////////////////////////////////////////

2개의 xml 파일

가. 설정파일
       - DB연동하기 위한 정보들을 포함한 파일.
       -  src
	    com
	      config
	          configuration.xml

나. mapper파일
       - SQL문이 저장된 파일.
       - 테이블당 하나씩 생성
         - src
	    com
	      config
	          DeptMapper.xml







String resource = "com/config/configuration.xml";
InputStream inputStream = Resources.getResourceAsStream(resource);
SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);