# DBMS_Study

Oracle

DBMS의 소통 방식
-----------------------------------------
     	      사용자
-----------------------------------------
   ↕ 	         ↕            ↕
고객 관리 응용프로그램      주문 관리 응용프로그램
   ↕ 	         ↕            ↕
-----------------------------------------
     	       DBMS
-----------------------------------------
RDBMS(관계형 데이터베이스 시스템)
	테이블끼리 서로 관계를 맺는다.
	
========================================

RDBMS(관계형 데이터베이스 시스템)
   테이블끼리 서로 관계를 맺는다.

Table A(Student, Member, User, People)      Table B(Order, Delivery)

번호(PK)   이름   나이   아이디(UK)      주문번호(PK)   번호(FK)   날짜      상품수량
1           오태양   19    oty1234  	   20230118001   3   2023-01-18   5
2           윤민우   18    ymu1234          20230118002   2   2023-01-18   1
3           임종욱   15    ljy1234             20221201001   3   2022-12-01   3
4           김은정   14    kyj1234            20221201003   1   2022-12-01   100
5           김주연   12    kjy1234            20221201002   5   2022-12-01   150


이러한 구조를 가지는 것을 Table, Relation(오라클), Class라고 부른다.

COLUMN(열, 속성, 필드)
ROW(행, 레코드, 튜플)

PRIMARY KEY(PK)
   고유한 값.
   각 행의 구분점으로 사용된다.
   중복이 없고 NULL값을 허용하지 않는다.

FOREIGN KEY(FK)Q
   다른 테이블의 PK를 의미한다.
   테이블끼리 관계를 맺을 때 사용한다.
   중복이 가능하다.

UNIQUE KEY(UK)
   NULL은 허용하지만 중복을 허용하지 않는다.

Scripts 새파일 생성 ctrl + ] 

------------------------------------------------------------------------------------------------

컴파일 언어와 스크립트 언어 

- 컴파일 언어	일괄적으로 전체 번역
	파일 단위로 해석한다(일괄 처리).
	부분 수정이 거의 없을 때 효율적이다.


- 스크립트 언어	개별적으로 일부분 번역
	한 줄 단위로 해석한다(개별 처리).
	빈번한 수정 시 효율적이다.	

SQL문 (쿼리문) - DDL, DML, DCL, TCL
	스크립트 언어.
	데이터베이스와 소통하는 언어.

- DDL (Data Definition Language) : 데이터 정의어	-> 복구 X
	테이블 조작, 제어 관련 쿼리문

	1. CREATE : 테이블 생성
		CREATE TABLE [테이블명] ([컬러명] [자료형(용량)] [제약조건], ... ); 

	2. DROP : 테이블 삭제
		DROP TABLE [테이블명];

	3. ALTER : 테이블 수정
		ALTER TABLE [테이블명]
	- 테이블명 수정 : RENAME TO [새로운 테이블명]
	- 컬럼 추가 : ADD([새로운 컬럼명] [자료형(용량)])
	- 컬럼명 변경 : RENAME COLUMN [기존 컬럼명] TO [새로운 컬럼명]
	- 컬럼 삭제 : DROP COLUMN [기존 컬럼명]
	- 컬럼 수정 : MODIFY([기존 컬럼명] [자료형(용량)])
	
	4. TRUNCATE : 테이블 내용 전체 삭제 
		TRUNCATE TABLE [테이블명]


------------------------------------------------------------------------------------------------

자료형(TYPE) : 용량은 항상 넉넉하게 주도록 한다.

	숫자 
		NUMBER
		NUMBER(n) : 정수
		NUMBER(n, m) : 실수 

	문자열 
		CHAR(n) : 고정형 / boolean으로 많이 표현된다.
	CHAR(4)에 'A'를 넣으면 A^^^ 빈 자리가 공백으로 채워진다.
	형식을 정한 날짜, 주민등록번호, 상태값 등 글자 수가 절대 변하지 않는 값을 넣는다.
		VARCHAR(n), VARCHAR2(n) : 가변형
	값의 길이만큼 공간이 배정된다. 글자 수에 변화가 있는 값을 넣는다.	

	날짜
		DATE 
	FORMAT에 맞춰서 날짜를 저장하는 타입
    
    
------------------------------------------------------------------------------------------------
    
    무결성
	데이터의 정확성, 일관성, 유효성이 유지되는 것.

	정확성 : 데이터는 애매하지 않아야 한다.
	일관성 : 각 사용자가 일관된 데이터를 볼 수 있도록 해야한다.
	유효성 : 데이터가 실제 존재하는 데이터여야 한다.

1. 개체 무결성	TABLE
	모든 테이블이 PK로 선택됨 컬럼을 가져야 한다.

2. 참조 무결성	FK
	두 테이블의 데이터가 항상 일관된 값을 가지도록 유지하는 것.

3. 도메인 무결성	COLUMN
	컬럼의 타입, NULL값의 허용 등에 대한 사항을 정의하고
	올바른 데이터가 입력되었는 지를 확인하는 것.


--------------------------------------------------------------------------------------------

모델링 (기획)
	추상적인 주제를 DB에 맞게 설계하는 것.

1. 요구사항 분석
	회원, 주문, 상품 : 3가지를 모두 관리하고 싶습니다.


2. 개념적 설계 (개념 모델링)
	회원		주문		상품
--------------------------------------------------------------------------

회원 번호			주문 번호		상품 번호 

회원 아이디		주문 날짜 	상품 이름
회원 비밀번호		회원 번호		상품 가격
회원 이름			상품 번호		상품 재고 
회원 주소			주문 개수 
회원 이메일		
회원 생일			
회원 핸드폰 번호 		


3. 논리적 설계 (논리 모델링)
회원			주문		상품

회원 번호 PK		주문 번호	 PK	상품 번호 PK 
회원 아이디 UK		주문 날짜 NN	상품 이름 NN
회원 비밀번호 NN		회원 번호	 FK	상품 가격 NN
회원 이름 NN		상품 번호	 KF	상품 재고 NN
회원 주소 NN		주문 개수 C, D(1)
회원 이메일 UK		
회원 생일			
회원 핸드폰 번호 UK	



4. 물리적 설계 (물리 모델링)
TBL_MEMBER		주문		상품
-------------------------

MEMBER_ID : NUMBER PK_MEMBER 

-------------------------

MEMBER_IDENTIFICATION : VARCHAR2 NOT NULL UNIQUE
MEMBER_PASSWORD : VARCHAR2 NOT NULL
MEMBER_NAME : VARCHAR2 NOT NULL
MEMBER_ADDRESS : VARCHAR2 NOT NULL
MEMBER_EMAIL : VARCHAR2 NOT NULL UNIQUE
MEMBER_BIRTH : DATE
MEMBER_PHONE : VARCHAR2 NOT NULL UNIQUE


5. 구현 

====================================================

DML (Data Manipulation Lagnuage)	CRUD

	1. SELECT : 조회 (검색)

		SELECT [컬럼명1, ....]
		FROM [테이블명]
		WHERE[조건식]
	
	2. INSERT : 추가

	1) 컬럼은 전부 다 작성하지 않아도 되고 필요한 컬럼만 작성할 수 있다.			INSERT INTO [테이블명] ([컬럼명, ...])
		VALUES ([값, ...])

	2) 모든 값을 전부 순서대로 작성해야 되며, 컬럼명은 직접 작성하지 않아도 된다.
		INSERT INTO [테이블명] 
		VALUES ([값, ...])

	3. UPDATE : 수정

		UPDATE [테이블명]
		SET [기존 칼럼명] = [값], [기존 칼럼명] = [값], ...
		WHERE [조건식]

	4. DELETE : 삭제

		DELETE FROM [테이블명]
		WHERE [조건식]

----------------------------------------------------------------------------------------

조건식 
	>, <		: 초과, 미만
	>=, <=		: 이상, 이하
	=		: 같다
	<>, !=, ^=	: 같지 않다.
	AND		: 둘 다 참이면 참
	OR		: 둘 중 하나라도 참이면 참

※ 위 연산자들은 WHERE 절에서 사용 가능하다.



----------------------------------------------------------------------------------------

TCL (Transaction Control Language) : 트랜젝션 제어어 

트랜젝션
	하나의 서비스를 구현하기 위한 DML의 묶음

COMMIT
	모든 작업을 확정하는 명령어

ROLLBACK
	이전 커밋한 지점으로 이동

**
TRUNCATE는 테이블 내용을 전체 삭제하므로, DELETE보다 빠르게 처리할 수 있다.
대용량 데이터 처리에 유리하지만 복구가 불가능하기 때문에 복구가 가능한 DELETE를 사용하는 것이 안전하다.

------------------------------------------------------------------------------------------------

NULL
	정의되지 않은 값.
	PK는 불가능, FK는 가능, UK도 가능

조건식 
	컬럼명 IS NULL : 컬럼값이 NULL이면 참
	컬럼명 IS NOT NULL : 컬럼값이 NULL이 아니면 참

NULL 값을 다른 값으로 변경
	NVL( 컬럼명, '값') : NULL 값 대신 다른 값으로 변경 후 조회
	NVL2( 컬럼명, 'NULL이 아닐 때 값', 'NULL일 때 값) 
	: NULL일 때의 값, NULL이 아닐 때의 값을 각각 설정

------------------------------------------------------------------------------------------------

정규화
	삽입/수정/삭제의 이상현상을 제거하기 위한 작업
	데이터의 중복을 최소화 하는 데에 목적이 있다.
	5차 정규화까지 있으나 3차 정규화까지만 진행한다.

1차 정규화
	같은 성격과 내용의 컬럼이 연속적으로 나타날 경우 

	상품명
	바지1, 바지2, 바지3

	상품명1	상품명2	상품명3
	바지1	바지2	바지3

	* 조회가 너무 힘들다 

	1차 정규화 진행
	
	상품명
	바지1
	바지2
	바지3

2차 정규화 
	조합키(복합키)로 구성되었을 경우 조합키의 일부분에만 종속되는 속성이 있을 경우	

	FLOWER
	이름	색상	꽃말	과
	해바라기	노란색	행운	국화
	장미	빨간색	사랑	장미

	* 이름에만 과가 종속됨

	2차 정규화 진행

	FLOWER
	이름	과	
	해바라기	국화	
	장미	장미	

	FLOWER_LANGUAGE
	이름	색상	꽃말	
	해바라기	노란색	행운	
	장미	빨간색	사랑	


	FLWOER의 PK를 이름으로 설정하고,
	FLOWER_LANGUAGE의 이름을 FK로 설정한다.
	FLOWER_LANGUAGE에서 이름을과 색상을 조합키로 설정한다.

3차 정규화
	PK가 아닌 칼럼이 다른 칼럼을 결정하는 경우
	이행함수 종속을 제거해야 한다.

	회원번호	이름	시	구	동	우편번호
	1	한동석	남양주	화도읍	구암리	12345
	2	홍길동	서울	관악ㅜ	봉천	55555


	* 우편번호로 시, 구, 동을 알 수 있다.
	* 중복된 데이터가 생길 가능성이 있다.

	회원번호	이름	우편번호
	1	한동석	12345
	2	홍길동	55555

	우편번호	시	구	동	
	12345	남양주	화도읍	구암리	
	55555	서울	관악구	봉천	

------------------------------------------------------------------------------------------------

데이터베이스에서 정규화가 필요한 이유

   데이터베이스를 잘못 설계하면 불필요한 데이터 중복으로 인해 공간이 낭비된다.
   이런 현상을 이상(Anomaly)현상이라고 한다.

   회원번호와 프로젝트코드 두 컬럼의 조합키로 설정되어 있는 테이블이고
   한 사람은 하나의 부서만 가질 수 있다.

   회원번호      이름   부서   프로젝트코드   급여   부서별 명수
   22080101   한동석   개발팀   ABC0001      3000   4
   22080101   한동석   개발팀   DEF1112      2000   4
   22080101   한동석   개발팀   CBA9474      4000   4
   22080104   홍길동   기획팀   EFG0881      5000   2
   22081106   이순신   디자인팀   GHI9991      6000   3

이상 현상의 종류
   - 삽입 이상
      새로운 데이터를 삽입하기 위해 불필요한 데이터도 삽입해야하는 문제
      
      담당 프로젝트가 정해지지 않은 사원이 있다면,
      프로젝트 코드에 NULL을 작성할 수 없으므로 이 사원은 테이블에 추가될 수 없다.
      따라서 '미정'이라는 프로젝트 코드를 따로 만들어서 삽입해야 한다.
   
   - 갱신 이상
      중복 행 중에서 일부만 변경하여 데이터가 불일치하게 되는 모순의 문제
   
      한 명의 사원은 반드시 하나의 부서에만 속할 수 있다.
      만약 "한동석"이 보안팀으로 부서를 옮길 시 3개 모두 갱신해주지 않는다면
      개발팀인지 보안팀인지 알 수 없다.

   - 삭제 이상
      행을 삭제하면 꼭 필요한 데이터까지 함께 삭제되는 문제

      "이순신"이 담당한 프로젝트를 박살내서 드랍된다면, "이순신" 행을 모두 삭제하게 된다.
      따라서 프로젝트에서 드랍되면 회사에도 드랍된다.

   2차 정규화 진행

   회원번호      이름   부서   부서별 명수
   22080101   한동석   개발팀   4
   22080104   홍길동   기획팀   2
   22081106   이순신   디자인팀   3   

   회원번호      프로젝트코드   급여
   22080101   ABC0001      3000
   22080101   DEF1112      2000
   22080101   CBA9474      4000
   22080104   EFG0881      5000
   22081106   GHI9991      6000

   3차 정규화

   회원번호      이름   부서
   22080101   한동석   개발팀
   22080104   홍길동   기획팀
   22081106   이순신   디자인팀

   부서   부서별 명수
   개발팀   4
   기획팀   2
   디자인팀   3   


------------------------------------------------------------------------------------------------

MySQL

MySQL 기초 문법
	- 데이터베이스 생성
		create database [데이터베이스명];

	- 데이터베이스 선택
		use [데이터베이스명];

	- CRUD 작성

MySQL 자료형
	- 정수
		tinyint
		smallint
		mediumint
		★ int
		bigint

	- 실수
		decimal (m, d) : m자리 정수, d자리 소수점으로 표현

	- 날짜
		date : 1000-01-01 ~ 9999-12-31
		time : -838:59:59 ~ 838:59:59
		datetime : 1000-01-01 00:00:00 ~ 9999:-12-31 23:59:59

	- 문자 
		char(m) : 고정 길이 문자열(0~255)
		varchar(m) : 가변 길이 문자열(0~65535)
