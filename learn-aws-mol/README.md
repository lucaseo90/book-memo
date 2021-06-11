# Learn AWS(Amazon Web Services) MoL(in aMonth of Lunches)

## 01

* 클라우드 컴퓨팅에 대한 소개
* 클라우드 컴퓨팅 제공 업체로서의 AWS에 대한 소개
* 책의 목적 및 구성
  > `Doing is more effective than reading`
* AWS의 리소스 배치 - Virtual Private Cloud (VPC)

## 02

* EC2 (Elastic Compute Cloud)
* EBS (Elastic Block Store)

### 실습
* EC2 Free tier 인스턴스 (Ubuntu 20.04 LTS) 생성
* AWS에서 제공하는 Web Console로 접속 
* LAMP 설치 (`$ sudo apt install lamp-server^`)
* `Hello World` 수준의 HTML 파일 추가하여 확인

#### 추가로 해봐야할 것
- [x] SSH로 접속
  1. 인스턴스 목록에서 접속하고자 하는 인스턴스 ID 클릭
  2. (우측 상단) 연결 클릭
  3. SSH 클라이언트 탭 클릭
  ```shell
  $ ssh -i keyname.pem ${USER_NAME}@${PUBLIC DNS}
  ```
  * 여기서 `.pem` 파일은 인스턴스 생성시 설정했던 key 파일 

## 03

* AWS가 가상화 하는 리소스
  * CPU: vCPU (v: virtual)
  * Storage: Elastic Block Store (EBS), 또는 S3 Storage
  * Memory
  * Network
* 애플리케이션의 요구 사항에 맞는 선택을 할 수 있도록 다양한 [인스턴스 유형](https://aws.amazon.com/ko/ec2/instance-types/)으로 세분화
  * 추가로 지리적인 요건을 고려하여 인스턴스가 배포될 지역을 선택 가능

### 실습
- [ ] WordPress 배포
  1. LAMP 설치
  2. MySQL 설치
  3. WordPress 다운로드 및 설정
  4. WordPress 파일을 Apache 루트 디렉토리로 복사
  5. WordPress 사이트 접속

## 04

* RDS (Amazon Relational Database Service)
  * EC2 기반 애플리케이션에 쉽게 통합 할 수 있는 데이터베이스 솔루션

### 실습
- [ ] RDS로 MySQL 데이터베이스에 저장한 데이터를 마이그레이션 

## 05

* Domain Name System (DNS)
* Route 53
  * Domain Registration
  * DNS Management
  * Traffic Management
  * Availability Monitoring

### 실습
- [ ] Route 53을 이용한 DNS 등록
