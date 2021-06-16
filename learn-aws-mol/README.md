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

## 06

* Simple Storage Service (S3)
  * Versioning 
  * Logging
  * Tags
  * User Management
  * Permission Management

### 실습
- [ ] WordPress에 포스트를 생성하는데, S3에 저장된 동영상을 URL 링크로 연결


## 07

* AWS에서 백업을 관리하는 방법
  1. EBS 볼륨 스냅샷(전체 사본)을 생성하여 S3에 저장
  2. 로컬 OS 도구를 사용하여 저장하고자 하는 데이터를 압축하여 S3에 저장
<br>

* AWS 환경에서 데이터 손상에 대한 위협 요소
  * Hacker: 데이터를 탈취하여 데이터에 대한 비용을 요구하는 주체
  * Admins: 인프라를 관리하다가 실수로 인해 중요한 설정 파일을 손상시키는 주체
    * 예) EC2 인스턴스 또는 데이터 볼륨을 삭제하는 경우
<br>

* 백업된 데이터는 복원했을 때 복원하는 시점으로부터 정상적으로 동작할 수 있는 형태로 관리

### 실습
- [ ] EBS 볼륨의 스냅샷을 생성하여 새로운 EC2 인스턴스에 연결하여 시작

## 08

* Identify and Access Management (IAM)
  * 리소스에 대한 정책, 사용자, 그룹 및 규칙을 정의

### 실습
- [ ] 사용자/그룹 조합을 만들고 정책을 검색 및 적용

## 09

* AWS를 사용하는 경우 비용은 Capital expenses (Capex) -> Operating expenses (Opex) 로 이동한다. 
  * Capex: 새로운 건물 및 서버와 같은 재화를 구매하기 위한 자본 비용  
  * Opex: 장비 대여 및 급여와 같은 지속적으로 발생하는 운영 비용

## 10

* AWS 내 관리해야하는 Resource가 많아지는 경우 Tag 및 Group을 지정하여 관리 가능

### 실습
- [ ] 두개 이상의 인스턴스를 생성하고, 각각 Tag를 지정한 후에 Grouping
