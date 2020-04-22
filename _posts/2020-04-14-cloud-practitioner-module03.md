---
layout: post
title:  "Cloud Practitioner"
date:   2020-04-14T09:25:52-00:00
author: dhp.lee
categories: Aws
tags: lorem
---

### AWS Integrated Services

Application Load Balancer
Classic Load Balancer에 몇 가지 중요한 기능 및 개선 사항 추가

향상된 기능
지원되는 요청 프로토콜 추가 (HTTP/2, WebSocket)
지표 및 액세스 로그 개선
상태 확인 대상 확대

추가 기능
경로 기반 라우팅
요청 내 URL을 기반으로 대상 그룹으로 라우팅하는 규칙 생성
호스트 기반 라우팅
동일한 로드 밸런서가 여러 도메인을 지원
요청된 도메인을 기반으로 요청을 대상 그룹으로 라우팅 가능
요청 추적: 클라이언트에서 대상까지 요청 추적
ECS 예약 컨테이너 사용 시 동적 호스트 포트 설정 가능
VPC에서 IPv6 기본 지원
AWS 웹 애플리케이션 통합

사용 시나리오
컨테이너를 사용하여 마이크로 서비스를 호스트하고 단일 로드 밸런서로부터 이러한 애플리케이션으로 라우팅
서로 다른 요청을 동일한 인스턴스로 라우팅하되 포트에 따라 다른 경로 지정 가능
다양한 포트에서 수신대기 하는 여러 컨테이너가 있을 경우 라우팅 규칙을 설정하여 원하는 백엔드 애플리케이션으로만 트래픽 분배 가능


Auto Scaling
기본 정보
애플리케이션의 로드를 처리할 수 있는 적절한 수의 EC2 인스턴스를 유지
향후 특정 시점에서 워크로드 요구 사항을 충족하기 위해 몇 개의 EC2 인스턴스가 필요할지 추측할 필요가 없어짐
CloudWatch를 통해 EC2 인스턴스의 워크로드 성능을 모니터링
자동 조정 구성 요소
시작 구성 생성 - WHAT
Auto Scaling이 시작할 인스턴스 정의
사용할 AMI, 인스턴스 유형, 보안 그룹, 역할 등
Auto Scaling 그룹 생성 - WHERE
배포가 이루어지는 위치와 배포에 대한 제한을 정의
어느 VPC가 인스턴스를 배포할지, 어느 로드 밸런서에서 상호 작용할지
인스턴스의 최소/최대 개수
Auto Scaling 정책 정의 - WHEN
언제 EC2 인스턴스를 시작/종료할지 지정
CloudWatch 경보를 통한 이벤트 설정


Amazon Route 53

도메인 이름시스템(도메인 솔루션)

IP 주소로 변환하는 데 이때 DNS가 필요, 관리

호스팅 영역 메인서버 4개 
FQDN 
DNS 등록 대행자 (개인정보 서비스 옵션)

고객과의 거래 단축, 이쿼리는 자동적으로 가장 가까운 노드에 찾아간다
가중치 기반 라운드 로빈, 지연 시간 기반 랑팅, 다중 응답

이 증가 고
성능증가 하고 고가영성 증가 아키텍처의 내결함성 감소
Ip4, Ip6 양쪽에도 쓸 수 있다


Amazon Relational Database Services(RDS)
기본 정보
운영 체제 설치 및 패치
데이터베이스 소프트웨어 설치 및 패치
자동 백업 및 고가용성 유지 관리
리소스 규모 조정
전력 및 서버 관리
유지 관리 수행
RDS의 기본 빌딩 블록은 데이터베이스 인스턴스
데이터베이스 인스턴스는 여러 데이터베이스가 포함 가능
MySQL, Amazon Aurora, MS Sequel Server, PostgreSQL, MariaDB, Oracle 등 6개 데이터베이스 지원
다중 가용 영역 배포로 높은 가용성 구현
마스터 데이터베이스 장애 발생 시 자동으로 예비 데이터베이스 인스턴스를 새 마스터로 가동
읽기 전용 복제본 생성 지원을 통한 성능 향상
읽기 전용 복제본은 마스터 데이터베이스와 다른 리전에 생성 가능


AWS Lambda
기본 정보
서버를 프로비저닝하거나 관리할 필요 없이 코드를 실행할 수 있는 컴퓨팅 서비스
필요할 때에만 코드 실행
초당 수천 건의 요청으로 자동 확장
코드가 실행되지 않는 시간에 대해서는 비용 발생하지 않음
모든 애플리케이션, 백엔드 서비스에 대한 코드 실행 가능
고가용성 컴퓨팅 인프라에서 코드 실행
서버 및 운영 체제 유지 관리, 용량 프로비저닝, Auto Scaling, 코드 모니터링, 로깅 등 모든 관리 기능 제공
다양한 프로그래밍 언어 지원
AWS CodePipeline, AWS CodeDeploy를 통해 자동 배포 가능
마이크로 서비스 아키텍처 구축
옵션
최대 512MB 디스크 공간
메모리 128MB ~ 3,008MB
최대 15분까지만 실행
최대 6MB의 요청 및 응답
최대 128KB의 이벤트 요청 본문
사용 예
백업 자동화
S3에 업로드된 객체의 처리
이벤트 중심의 로그 분석
이벤트 중심의 변환
IoT
서버리스 웹사이트 운영
Amazon Kinesis를 통한 실시간 스트리밍 데이터 처리
애플리케이션 활동 추적
트랜잭션 주문 처리
클릭스트림 분석
데이터 정리 측정치
생성 로그 필터링
소셜 미디어 인덱싱 분석
디바이스 데이터 원격 측정 및 모니터링


Elastic Beanstalk
기본 정보
PaaS
앱을 빠르게 배포
관리의 복잡성 감소
제어 권한 유지

Java, .NET, PHP, Node.js, Python, Ruby, Go, Docker를 사용하여 Apache, Nginx, Passenger, IIS 같은 친숙한 서버에서 개발된 웹 애플리케이션 및 서비스를 배포하고 확장하는 서비스
전체 시스템을 완벽하게 제어 가능
용량 프로비저닝
로드 밸런싱 (HTTPS 활성화 가능)
Auto Scaling
애플리케이션 상태 모니터링
사용 중인 애플리케이션 업데이트 가능
서버 로그 파일 액세스 가능


Amazon Simple Notification Service(SNS)

유연한 완전관리형 게시/구독 메시징 및 모바일 통신 서비스
구독 엔드포인트 및 클라이언트로의 메시지 전달을 조율
안정적인 통신을 손쉽게 설정, 운영 및 전송할 수 있음
마이크로서비스, 분산 시스템 및 서버리스 애플리케이션을 분리 및 확장할 수 있음


Amazon CloudWatch
기본 정보
모니터링 서비스
지표 수집 및 추적
로그 파일 수집 및 모니터링
경보 설정
AWS 리소스 변경에 자동 대응
AWS 리소스 뿐만 아니라 애플리케이션과 서버에서 생성된 사용자 정의 지표 및 애플리케이션에서 생성된 모든 로그 파일 모니터링 가능
시스템 전반의 리소스 사용률, 애플리케이션 성능, 운영 상태 파악을 통해 문제에 대응하고 애플리케이션 실행을 원활하게 유지 가능

CPU 사용률이 5분동안 60%를 초과하는 경우
동시 연결수가 1분 동안 10을 초과하는 경우
정상 호스트 수가 10분동안 5미만인 경우

CloudWatch 콘솔에서 사용자 지정 가능한 홈페이지를 통해 단일 뷰에서 리소스를 모니터링 할 수 있습니다.
- 다른 리전에 분산되어 있는 리소스도 가능합니다.
AWS 리소스에 대한 지표 및 경보의 사용자 지정 뷰를 생성할 수 있습니다.
- 각 대시보드는 여러 지표를 표시할 수 있으며, 텍스트와 이미지로 꾸밀 수 있습니다.
콘솔, AWS CLI 또는 PutDashboard API를 사용하여 대시보드를 생성할 수 있습니다.



Amazon CloudFront



