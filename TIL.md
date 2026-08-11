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
* github 담당자로서 팀원들의 pr을 합치는 과정에서 conflict 발생 -> 추후 배우고 방법 찾기
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

* 
