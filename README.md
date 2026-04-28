# Oracle 19c에서 PostgreSQL로 데이터 이행 (Ora2Pg)

Oracle 19c에서 PostgreSQL 15로 데이터를 이행하는 가이드입니다.

---

## 실습 환경

| 항목 | 값 |
|------|-----|
| OS | Oracle Linux 7.9 |
| Oracle | 19c EE (Non-CDB), SID=orcl |
| Oracle IP | 192.168.23.67 |
| Oracle Home | /u01/app/oracle/product/19.3.0/dbhome_1 |
| PostgreSQL | 15.17, Port=5432 |
| 타겟 DB | testdb |

---

## 이행 방법 비교

| 방법 | 특징 | 활용도 |
|------|------|--------|
| Ora2Pg | Perl 기반 / 스키마 DDL 변환 + 데이터 이관 + PL/SQL 변환 지원 | 높음 |
| pgloader | 한 줄 명령으로 실행 / 데이터 위주 | 낮음 |
| CSV 우회 | spool → COPY / 개념 이해용 | 낮음 |

> 본 실습은 Ora2Pg를 사용한다. 타입 매핑, 스키마 변환, 데이터 이관, 리포트까지 전 과정을 다루기 때문이다.

---

## 설치 순서

| 순서 | 문서 | 설명 |
|------|------|------|
| 1 | [Oracle SCOTT 스키마 이행](./1.%20Oracle%20SCOTT%20스키마%20이행.md) | Ora2Pg 설치 및 SCOTT 스키마 이행 |
| 2 | [Oracle HR 스키마 이행](./2.%20Oracle%20HR%20스키마%20이행.md) | 시퀀스/트리거 포함 HR 스키마 전체 이행 |
| 3 | [DBeaver로 PostgreSQL 접속](./3.%20DBeaver로%20PostgreSQL%20접속.md) | 이행 완료 후 DBeaver 접속 확인 |

---

## 주요 특징

- Oracle 19c SCOTT / HR 스키마 전체 오브젝트 이행
- Ora2Pg를 활용한 DDL 자동 변환 및 데이터 이관
- 이관 난이도 리포트(SHOW_REPORT) 생성 및 분석
- 순환 FK 처리 및 시퀀스 Last Value 동기화
- Oracle / PostgreSQL 데이터 건수 및 제약 조건 검증

