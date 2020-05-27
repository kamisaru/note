## ETL JOB LOGS 
ETL 작업 시 처리에 대한 로그를 남기기 위한 쉘 스크립트 및 기타 파일을 관리 하기 위한 프로젝트

### 프로젝트 구조 
root

 |- script
 
 |   | - before_logging.sh          ETL 작업 시작 로그를 등록 하는 Shell
 
 |   | - after_logging.sh           ETL 작업 종료 로그를 등록 하는 Shell
 
 |   | - email_post.sh              로깅 작업 중 오류 시 E-mail을 발송 하는 Shell
 
 |- template/email_template.html    E-mail 템플릿
 
 |- ddl/etl_logs.sql                Table DDL
