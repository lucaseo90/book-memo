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

## 11

* AWS Budgets
  1. 예산 이름 지정 
  2. 비용 또는 사용량을 선택
  3. 예산 기간 설정
  4. 예산의 활성 상태 설정
  5. 알람이 트리거 되기 전에 기간동안 지출할 최대 금액의 예산 설정
* AMAZON Simple Notification Service (SNS)
* CloudWatch

### 실습
- [ ] 실행중인 모든 리소스 중에 일부 리소스에만 집중하는 예산 + 알림 적용

## 12

* AWS CLI

### 실습
- [ ] AWS CLI를 설치 및 활용

## 13

* AWS에서의 High Availability (HA)를 위한 구성요소
  1. Virtual Private Cloud (VPC)
  2. Private and Public subnet
  3. Security
  4. EC2 AMI (Amazon Machine Image)
  5. S3 Bucket
  6. EBS Volume
  7. Auto Scaler
  8. Load Balancer

> AWS 서비스의 이름 (EC2, ECS, EFS, EMR 등)에서의 E의 의미는 email의 electronic이 아닌 elastic을 의미한다. 

* 클라우드 컴퓨팅이 제공해야하는 특성 - 미국 NIST에서 정의한 특성
  * On-demand self-service
  * Broad network access
  * Resource pooling
  * Rapid elasticity
  * Measured service

## 14

* AWS Virtual Private Cloud (VPC)
  * high configurable routing
  * access-control
  * networking tool

> VPC에서 EC2 인스턴스를 시작하면, VPC의 보안 및 연결 설정이 자동으로 상속된다.

### 실습
- [ ] 2개 이상의 서브넷이 있는 VPC를 만들고, 동일한 EC2 인스턴스를 배포한 뒤 둘 다 사용가능한지 확인

## 15

* ELB (Elastic Load Balancing)

### 실습
- [ ] AMI를 여러 인스턴스 애플리케이션 로드밸런서에 배포하고, 인스턴스가 실패할때 얼마나 빨리 로드밸런서가 복구되는지 확인

## 16

* Auto Scaling
  * Auto: 사람의 개입 없이 일어나는 것
  * Scaling: 필요에 따라 용량(capacity)가 확장 또는 축소

* AWS에서 Auto Scaling 설정
  1. `Launch Configuration`에서 Auto Scaler가 새 인스턴스가 필요할 때 시작할 AMI를 선택
  2. 인스턴스의 유형을 선택 (예: `t2.micro`)
  3. 설정에 이름을 지정
  4. 저장소 및 보안 그룹 단계 수행
  5. `Create Auto Scaling Group` 페이지에서 Auto Scaling 그룹 생성
  6. 로드밸런서가 사용하는 대상 그룹을 지정
  7. 인스턴스를 확장 및 축소하기 위한 정책 설정

### 실습
- [ ] Auto Scaling 구성을 하여, 인스턴스를 강제로 종료시킬 때 현상을 확인
- [ ] WordPress의 데이터베이스를 RDS로 변경하고, WordPress 설치가 데이터베이스와 연결되는 새로운 AMI를 생성
  * MySQL은 각 인스턴스에 종속적이기 때문에 새로운 인스턴스가 실행되었을때 데이터 일관성을 위해 필요

## 17

* Content-Delivery Network (CDN) - *edge caching*
* CloudFront
* Transport Layer Security (TLS)
* Time-to-Live (TTL)


