# DataBase_Practice

## Use Data Base
1. `Data Base?`= 데이터를 표 형식으로 표현한 테이블의 집합체
2. `DBMS?` = DBMS란 사용자와 데이터베이스 사이에서 사용자의 요구에 따라 정보를 생성해주고 데이터베이스를 관리할 수 있게 해주는 소프트웨어
3. `Use Data Base` = Oracle DB
4. `Use DBMS` = SQL Developer

## Oracle pros and cons
`장점`
1. PC급에서 Mainframe급까지 모두 설치가능
2. 3rd Party의 강력한 지원
3. 분산처리 지원 기능의 우수성
4. SMP 및 MPP의 지원

`단점`
1. DBMS를 운영하기 위하여 많은 하드웨어 자원의 필요
2. 복잡한 DBMS 관리
3. 가격이 동종의 DBMS보다 비싸며 모든 제품에 Kernel이 필요
4. 배우기 힘든 제품 기능들의 존재

## Constraint  
1. `Primary Key` = 다른 항목과 절대로 중복되어 나타날 수 없는 단일 값을 가진 기본키
2. `Foreign Key` = 두 테이블을 서로 연결하는 데 사용되는 외래키다.

## Create Table, Modify Table
```
CREATE TABLE STADIUM (   /* 경기장 테이블 생성 */
STADIUM_ID CHAR(3) NOT NULL, /* 경기장_ID 고정길이(3) 필수 값 */
STADIUM_NAME VARCHAR2(40) NOT NULL, /* 경기장_이름 가변길이(40) 필수 값 */
HOMETEAM_ID CHAR(3), /* 홈팀_ID 고정길이(3) */
SEAT_COUNT NUMBER, /* 좌석 수 숫자타입 */
ADDRESS VARCHAR2(60), /* 주소 가변길이(60) */
DDD VARCHAR2(3), /* ddd 가변길이(3) */
TEL VARCHAR2(10), /* 전화번호 가변길이(10) */
CONSTRAINT STADIUM_PK PRIMARY KEY (STADIUM_ID) /* 제약조건 경기장_PK : 경기장_ID를 고정키로 지정 */
);

CREATE TABLE TEAM (  /* 팀 테이블 생성 */
TEAM_ID CHAR(3) NOT NULL, /* 팀_ID 고정길이(3) 필수 값 */
REGION_NAME VARCHAR2(8) NOT NULL, /* 지역_이름 가변길이(8) 필수 값 */
TEAM_NAME VARCHAR2(40) NOT NULL, /* 팀_이름 가변길이(40) 필수 값 */
E_TEAM_NAME VARCHAR2(50), /* E_팀_이름 가변길이(50) */
ORIG_YYYY CHAR(4), /* ORIG_YYYY 가변길이(4) */
STADIUM_ID CHAR(3) NOT NULL, /* 경기장_ID 고정길이(3) 필수 값 */
ZIP_CODE1 CHAR(3), /* ZIP_CODE1 고정길이(3) */
ZIP_CODE2 CHAR(3), /* ZIP_CODE2 고정길이(3) */
ADDRESS VARCHAR2(80), /* 주소 가변길이(80) */
DDD VARCHAR2(3), /* DDD 가변길이(3) */
TEL VARCHAR2(10), /* 전화번호 가변길이(10) */
FAX VARCHAR2(10), /* 팩스 가변길이(10) */
HOMEPAGE VARCHAR2(50), /* 홈페이지 가변길이(50) */
OWNER VARCHAR2(10), /* 오너 가변길이(10) */

CONSTRAINT TEAM_PK PRIMARY KEY (TEAM_ID), /* 제약조건 팀_PK : 팀_ID를 기본키로 지정 */
CONSTRAINT TEAM_FK FOREIGN KEY (STADIUM_ID) REFERENCES STADIUM(STADIUM_ID) ); 
/* 제약조건 팀_FK : 경기장_ID를 외래키로 지정 참조할 테이블은 경기장, 참조할 컬럼은 경기장_ID */

CREATE TABLE SCHEDULE ( /* 테이블 SCHEDULE 생성 */
STADIUM_ID   CHAR(3) NOT NULL,
SCHE_DATE    CHAR(8) NOT NULL,
GUBUN        CHAR(1) NOT NULL,
HOMETEAM_ID  CHAR(3) NOT NULL,
AWAYTEAM_ID  CHAR(3) NOT NULL,
HOME_SCORE   NUMBER(2),
AWAY_SCORE   NUMBER(2),
CONSTRAINT SCHEDULE_PK PRIMARY KEY (STADIUM_ID, SCHE_DATE),
CONSTRAINT SCHEDULE_FK FOREIGN KEY (STADIUM_ID) REFERENCES STADIUM(STADIUM_ID)
);

CREATE TABLE PLAYER ( /* 테이블 플레이어 생성 */
PLAYER_ID CHAR(7) NOT NULL, /* 플레이어_ID 고정길이(7) 필수 값 */
PLAYER_NAME VARCHAR2(20) NOT NULL, /* 플레이어_이름 가변길이(20) 필수 값 */
TEAM_ID CHAR(3) NOT NULL, /* 팀_ID 고정길이(3) 필수 값 */
E_PLAYER_NAME VARCHAR2(40), /* E_플레이어_이름 가변길이(40) */
NICKNAME VARCHAR2(30),  /* 별명 가변길이(30) */
JOIN_YYYY CHAR(4), /* 조회_YYYY 고정길이(4) */
POSITION VARCHAR2(10), /* 포지션 가변길이(10) */
BACK_NO NUMBER(2), /* 백_넘버 숫자타입 */
NATION VARCHAR2(20), /* 국가 가변길이(20) */
BIRTH_DATE DATE, /* 생년월일 날짜타입 */
SOLAR CHAR(1), /* SOLAR 고정길이(1) */
HEIGHT NUMBER(3), /* 키 숫자타입(3) */
WEIGHT NUMBER(3), /* 몸무게 숫자타입(3) */
CONSTRAINT PLAYER_PK PRIMARY KEY (PLAYER_ID), /* 제약조건 플레이어_PK : 플레이어_ID 기본키로 지정 */
CONSTRAINT PLAYER_FK FOREIGN KEY (TEAM_ID) REFERENCES TEAM(TEAM_ID) ); 
/* 제약조건 플레이어_FK : TEAM_ID 외래키로 지정 참조 테이블은 팀, 참조할 컬럼은 팀_ID */

/*ALTER TABLE 테이블명 ADD 추가할 칼럼명 데이터 유형;*/

/* 1. add 2. drop 3. modify 4.rename*/

ALTER TABLE PLAYER ADD test2 varchar(20); /* 수정 플레이어 테이블에 test2 가변길이(20)을 추가 */
ALTER TABLE PLAYER DROP COLUMN test2; /* 수정 플레이어 테이블에 컬럼 test2를 삭제 */
ALTER TABLE PLAYER MODIFY test3 varchar(50) null; /* 수정 플레이어 테이블 컬럼변경 test3의 가변길이(50) null값은 허용 */
ALTER TABLE PLAYER RENAME COLUMN test2 to test3; /* 수정 플레이어 테이블의 컬럼 test2를 test3로 이름변경 */

select * from Player; /* 플레이어 테이블의 모든 내용을 보기 */
```

## Table entity-relationship Diagram!
![Relational_1](https://user-images.githubusercontent.com/83123393/141449694-f8ab7317-a6cb-4102-8a91-37878a7cbb3c.png)
