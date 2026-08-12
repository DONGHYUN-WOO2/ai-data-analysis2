# 8/10 TIL
## 1주차 팀프로젝트
맡은 일 : github 관리 및 자료 통합
* github repository 만들고, 팀원들 collatorator로 추가 -> 팀원들이 저장소에 접근해서 push 가능해짐
* main 브랜치 만들고, 팀원들은 원격 브랜치 만들기. 
* 저장소 구조 만들고(틀),가상환경(venv), gitignore, requirement.txt 만들고 push -> 팀원들은 pull해서 사용
venv 명령어 [python -m venv .venv]
requirement.txt 앱 설치 명령어 [python -m pip install -r requirement.txt]
확인 명령 [git remote -v][git status][python -c "import pandas, streamlit; print('환경 확인 완료')"]
* Issue 작성
* main 관련 명령어 [git switch main][git pull origin main] -> git pull origin main으로 하는게 실수할 확률이 적으므로 메인으로 쓸 것

어려웠던 점 
* 코드가 익숙치 않아 헤메는 부분이 있었음 
* github 담당자로서 팀원들의 pr을 합치는 과정에서 conflict 발생 -> 충돌 발생한 부분에서 current change를 받아들이고 다시 커밋한다. 
* 자꾸 메인에서 작업하는 실수가 있었음 -> switch 명령어보다는 pull orgin을 메인으로 사용할 것 

# 8/11 TIL
## 데이터베이스 

PostgreSQL = 데이터를 저장하는 창고(DB) -> 설치하면 이제 내 컴퓨터가 DB서버가 됨
DBeaver    = 창고 안을 편하게 관리하는 프로그램(리모컨) - DB안에서 값을 쉽게 찾고 정리할 수 있게 해주는 GUI툴(보기 쉽게)

PostgreSQL

└── Databases

    └── postgres

        └── Schemas

            └── public

비유하면 
PostgreSQL Server = 아파트 단지
Database          = 아파트 한 동
Schema            = 한 동 내부의 구역
Table             = 실제 물건을 보관하는 서랍

## CRUD - 데이터베이스에서 가장 기본이 되는 작업
* create - 데이터 추가

INSERT INTO practice.members (name, email, age)

VALUES ('홍길동', 'hong@example.com', 25);

* 여러명 한번에 추가 

INSERT INTO practice.members (name, email, age)

VALUES

('김영희', 'younghee@example.com', 31),

('이철수', 'chulsoo@example.com', 28),

('박민지', 'minji@example.com', 23);

* read - 전체 데이터 조회
  
select *  -> *는 전체. 일부만 조회하고 싶으면 * 대신 다른 값(ex.name, email) 넣으면 됨

from practice.members;

* 이름으로 특정 회원 찾기

select *

from practice.members

where name = '홍길동';

* update - 데이터 수정하기 

update practice.members

set age = 26

where name = '홍길동';

* delete - 데이터 삭제하기

먼저 삭제한 데이터 확인. 

SELECT *

FROM practice.members

WHERE name = '박민지';

그 후 삭제

DELETE FROM practice.members

WHERE name = '박민지';

** 여기서 중요한 부분! update나 delete 할때 where를 지정하지 않으면, 데이터 값 전체가 수정되거나 삭제될 수 있으므로 where으로 어떤 데이터가 선택되는지 확인하는게 좋다. 

# 8/12 TIL

## 2주차 팀프로젝트 제안서 작성
- 역할 배분. 
  평가 진행 로직 (팀평가/개인평가)
단계

1. EvaluationTemplate, EvaluationQuestion 모델 (5점 척도 문항)
2. TeamEvaluation/PeerEvaluation 및 응답 모델
3. 평가 폼 화면 (제출 기능까지, 디자인은 나중)
4. BR-01~05 규칙을 서버 로직 또는 unique_together로 강제 (자기 팀 평가 불가, 자기 자신 평가 불가, 중복 제출 불가)
5. 실제로 규칙을 우회 시도해보며 테스트 (본인 팀 평가 시도 → 막히는지, 같은 평가 두 번 제출 → 막히는지)


### 유의점 / 집중할 프로세스

- 이 파트가 5개 역할 중 비즈니스 규칙이 제일 많이 몰리는 곳이라 AI에게 코드를 요청할 때 "자기 팀/자기 자신 평가를 막아주세요"라고 막연히 요청하지 말고, 구체적인 케이스를 하나씩 나열해서 요청할 것
- 4단계(규칙 구현)까지 끝나야 양성용이 점수 계산을 테스트할 수 있으므로, 팀 내 병목 지점임을 인지하고 우선순위를 높게 잡을 것


## Django + PostgreSQL 실습
crud. create - insert / read - select / update / delete

Dbeavers의 스키마\practice\members 에 데이터 값을 만든다.
이후 동일하게 프로젝트 작업 폴더를 따로 만들고, 가상환경 세팅 

mkdir로 만들거나, 손으로 dev 안에 django_members 폴더를 만든 후 cmd에서 vs code로 연다.

이후 가상환경 -> python -m venv .venv
활성화 -> venv\scripts\activate.ps1

가상환경을 활성화 한 후 django와 postgresql 드라이버 설치

pip install django "psycopg[binary]" python-dotenv

pip list #설치확인

pip freeze > requirements.txt #설치된 것들을 txt로 만든다. 

프로젝트 생성

django-admin startproject config .
-> congig가 만들어짐

