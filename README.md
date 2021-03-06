# EricssonAutoHealthCheck
무선 통신 장비 온도/무선레벨/QAM 등 점검요소 자동 수집 툴

### 개발기간
    2020.06~2020.09(4개월)   
    
### 개발인원
    1인 개발

### 내용
    SK텔레콤 서해도서 Ericsson 무선 통신 장비 온도/무선레벨/QAM 등 점검요소 자동 수집 툴
    
### 개발배경   
    - 수도권 관제팀 자체 E-MW 운용 DB 누적 관리를 위해 Weekly MW 장비 온도, 무선레벨, SNR 값 관리하고 있었음   
    - 기존 방식은 노드 일일이 접속 후 온도, 무선레벨, SNR 값 확인하여 수기 엑셀 입력으로 소요시간은 360분으로 비효율적   
    - 주 1회 시행으로 2주 후 수도권 관리 대상 전체 노드의 정보를 수집 할 수 있었음   
   
### 목적   
    - 수동적인 비효율 업무 개선   
    - 수집 데이터양 증대   
    - RM 발췌/개선 : 장애 발생 가능성 높은 구간 분석시 백데이터로 활용   
   
### 개발 중 문제점 및 해결   
    - SecureCRT 제공 라이브러리 호환 문제 - 터미널 제어 로직으로 변경 후 해결   
    - 커맨드 결과 텍스트가 비동기식으로 일부 누락되는 문제 - 커맨드 결과를 받을 때까지 listen하도록 하여 해결   
   
### 개선효과   
    - 시간   
        ㅇ개선 전 : 수동, 약 360분 소요
        ㅇ개선 후 : 자동, 약 60분 소요
        ㅇ효과 : 약 300분 절약 및 인력 효율화(타 주요 업무 수행가능)
    - 데이터
        ㅇ개선 전 : 모든 노드 데이터 수집에 2주 소요
        ㅇ개선 후 : 매일 06:00 기준 필요 데이터 자동 수집 후 DB화(엑셀)
        ㅇ효과 : 수집 데이터량 약 336배 증가(2주 분량 1시간내 수집)
### 결과
    - 노드 NPU 온도 값, 무선 레벨 값, 변조 방식(QAM) 데이터 수집
    - 작업 스케줄링 활용 06:00 기준 전체 노드 순회하며, 데이터 수집
    - One-Click화 개발 : 더블클릭만으로 동작
    - 노드 접속 불가, QAM 값 미지원 MMU 사용 중, 1+0 운용 중 등 발생 가능 상황에 대해 예외 처리 구현
    - 09/17 ~ 09/23 8일간 Tool 테스트시 특이사항 없음
 
### 동작방식
    - 파이썬 Telnetlib 모듈 활용 원격 노드 접속
    - Command 입력
    - Command 결과 텍스트 추출
    - 텍스트내 필요 데이터 파싱
    - 데이터 가공
    - 데이터 테이블화
    - 상기 로직 반복하여 모든 노드 순환
    - 엑셀로 저장
    
### 활용 라이브러리
    - telnetlib
    - pandas
    - pyinstaller
