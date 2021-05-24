# Learn K8s(Kubernetes) MoL(in a Month of Lunches)

## 01

### memo
<details><summary>CLICK ME</summary>
<p>


Kuberntes는 컨테이너를 실행하기 위한 플랫폼으로 컨테이너화(containzred)된 애플리케이션을 위해 아래와 같은 기능을 제공한다.
* 컨테이너화된 애플리케이션의 실행
* 순차적 업데이트
* 서비스 레벨 유지 
* 수요에 따른 스케일 확장
<br><br>

Kubernetes에는 두개의 핵심 개념이 있다.
1. 애플리케이션 정의를 위한 `API`
2. 애플리케이션 실행을 위한 `클러스터`
<br><br>

YAML 파일에 앱을 정의하고 Kubernetes에 전달함으로써, Kubernetes는 YAML 파일에 정의된 항목을 수행한다. 
* 사용자는 애플리케이션의 구조를 정의하는 역할
* 정의된 애플리케이션의 실행 및 관리는 Kuberntes의 역할
* YAML 파일을 애플리케이션을 제공하는 모든 컴포넌트의 목록을 담고있는 의미에서 애플리케이션 `매니페스트(manifest)`라고도 부름
  > 매니페스트 파일(manifest file)은 컴퓨팅에서 집합의 일부 또는 논리정연한 단위인 파일들의 그룹을 위한 메타데이터를 포함하는 파일이다. - wikipedia (1)

<br>

Kubernetes 클러스터에는 분산데이터베이스가 있다.
* 애플리케이션에 대한 설정 파일과 API 키 그리고 연결 자격 증명과 같은 데이터를 저장
* Kubernets 클러스터 데이터는 etcd라는 일관적이고 고가용성을 갖는 key-value 저장소를 사용 (2)
<br><br>


</p>
</details>

### practice
<details><summary>CLICK ME</summary>
<p>
  
  
실습을 위한 Kubernetes 구성이 필요한데, macOS 기준으로 [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-mac) 설치 후 Dashboard에서 kubernetes를 활성화할 수 있다. 

```shell
$ kubectl get nodes
NAME             STATUS   ROLES    AGE   VERSION
docker-desktop   Ready    master   13d   v1.19.3
```


</p>
</details>

### 추가 Reference
1. [매니페스트 파일](https://ko.wikipedia.org/wiki/%EB%A7%A4%EB%8B%88%ED%8E%98%EC%8A%A4%ED%8A%B8_%ED%8C%8C%EC%9D%BC)
2. [쿠버네티스 컴포넌트 - etcd](https://kubernetes.io/ko/docs/concepts/overview/components/#etcd)

## 02

### memo
<details><summary>CLICK ME</summary>
<p>
  
  
Kubernetes는 컨테이너를 클러스터의 단일 노드에서 실행되는 컴퓨팅 단위인 Pod로 래핑한다. 
* Pod에는 Kubernetes에서 관리하는 가상 IP 주소를 할당
* Pod는 단일 컨테이너 또는 다수의 컨테이너 실행이 가능
* Kubernetes는 컨테이너를 직접 실행하지 않고, 노드에 설치된 도커와 같은 컨테이너 런타임에 위임
  * Pod의 컨테이너 ID는 컨테이너를 실행하는 다른 시스템에 대한 참조 
  * CRI(Container Runtime Interface)라는 API를 이용

Controller는 다른 리소스를 관리하는 Kubernetes의 리소스다. 
* Kubernetes API와 함께 시스템의 현재 상태를 관찰하여 리소스 상태에 따라 필요한 부분을 변경
* 다양한 Controller가 있으며, Pod 관리를 위한 주요 컨트롤러로 `Deployment`가 존재
* Controller는 라벨 선택기(label selector)를 사용하여 관리하는 리소스를 식별
  * 라벨을 활용한 리소스 식별
* Controller를 통해 Pod가 할당되는 경우, Controller 부터 리소스 해제
  * Controller는 Pod를 관리하는 주체로, 관리 중인 Pod가 삭제되면 다시 복구

애플리케이션 매니페스트는 JSON 또는 YAML로 작성할 수 있다.
* 선언적으로 작성되어 Kubernets에 원하는 최종 결과를 알리고, 이를 위해 수행해야 할 작업을 결정
* 애플리케이션에 대한 복제본 수, 적용해야하는 자원 제한, 정상 구동 여부, 애플리케이션의 설정 및 데이터를 저장하는 위치등을 지정 가능
  ```yaml
  # Kubernetes API의 버전과 리소스 유형을 지정
  apiVersion: v1
  kind: Pod

  # 리소스에 대한 메타데이터에는 이름(필수) 및 라벨(선택 사항)을 지정 
  metadata:
    name: hello-kiamol-3

  # 스펙은 리소스에 대한 실제 스펙으로, Pod의 경우 최소한 컨테이너 이름 및 이미지와 함께 실행할 컨테이너를 지정 
  spec:
    containers:
      - name: web
        image: kiamol/ch02-hello-kiamol
  ```

</p>
</details>

### practice
<details><summary>CLICK ME</summary>
<p>
  
#### Pod 생성
```shell
$ kubectl run ${POD_NAME} --image=${IMAGE} ${OPTIONS}
```

#### Pod 조회 및 접근
```shell
$ kubectl get pods
$ kubectl get pod ${POD_NAME}
$ kubectl describe pod ${POD_NAME}

# Pod 접속
$ kubectl exec -it ${POD_NAME} -- sh

# Pod 로그 확인
$ kubectl logs ${POD_NAME}
```

#### Pod 삭제
```
$ kubectl delete pod ${POD_NAME}
$ kubectl delete pods --all
```

</p>
</details>

## 03
<details><summary>CLICK ME</summary>
<p>


Kubernetes는 Pod에 가상 환경의 IP 주소를 할당한다.
* Pod는 해당 IP 주소를 통해 Pod 간의 통신을 수행
* Pod의 IP는 Kubernetes API를 통해 검색

Kubernetes는 IP 주소에 서비스 이름을 매핑하기 위해 DNS 서버를 내장한다.
* 서비스에는 자체 IP 주소가 있으며, 사용자가 해당 주소로 요청하면, Kubernetes는 Pod의 실제 IP 주소로 라우팅
* 서비스와 Pod간의 링크는 Deployment와 Pod간의 링크와 같이 레이블 선택기로 설정

Kubernetes의 기본 서비스 타입은 ClusterIP로 구성된다.
* 모든 노드의 Pod가 액세스 할 수 있는 클러스터 전체 IP 주소를 생성
* IP 주소는 클러스터 내에서만 작동하며, Pod간 통신에 활용

LoadBalancer 타입의 서비스는 트래픽을 수신한 노드와 다른 노드에서 실행 중일 수 있는 Pod로 트래픽을 가져오도록 한다.
  ```yaml
  apiVersion: v1
  kind: Service
  metadata:
    name: numbers-web
  spec:
    ports:
      - port: 8080      
        targetPort: 80  
    selector:
      app: numbers-web
    type: LoadBalancer  
  ```
  * 포트 8080을 이용해 수신 대기하고, 포트 80의 Pod로 트래픽을 전달하는 LoadBalancer 서비스
  * 외에 로드밸런서에 의존하지 않는 NodePort 서비스도 존재
 
Kubernetes에서 외부로 트래픽 전달을 위해서는 ExternalName 서비스를 사용할 수 있다.
* 애플리케이션 Pod에서 로컬 이름을 사용 가능
* Kubernetes의 DNS 서버각 Pod 조회 요청시 해당 로컬 이름을 정규화된 외부 이름으로 확인
* DNS의 표준 기능인 CNAME(Canonical NAMEs)을 사용하여 구현
* 다른 옵션으로는 headless 서비스가 존재


</p>
</details>

### practice
<details><summary>CLICK ME</summary>
<p>

#### 예제 Service (`sleep2-service.yaml`)
```yaml
apiVersion: v1  
kind: Service

metadata:
  name: sleep-2 

spec:
  selector:
    app: sleep-2
  ports:
    - port: 80
```

#### Service 생성
```shell
$ kubectl apply -f sleep2-service.yaml
```

#### Service 조회
```shell
$ kubectl get svc ${SERVICE_NAME}
```

#### Service
```shell
$ kubectl delete svc ${SERVICE_NAME}
```

</p>
</details>

## 04
<details><summary>CLICK ME</summary>
<p>


Kubernetes는 ConfigMap 및 Secrets로 설정을 지원한다.
* ConfigMap은 Pod에 로드할 수 있는 일부 데이터를 저장하는 리소스
* ConfigMap이 Pod에 적용되는 시점은 애플리케이션에 다를 수 있지만, 주로 Pod가 교체하면서 적용
* Secrets는 디스크가 아닌 메모리에 저장되며, Kubernetes 내에서 권한제어 및 암호화
* Secrets에 권한이 있는 사람은 평문인 값을 확인 가능

</p>
</details>

## 05

### memo
<details><summary>CLICK ME</summary>
<p>


Kubernetes에는 Pod 지원을 위한 파일시스템이 존재한다. 
* 기본적으로 Pod에 대한 데이터는 영속적이지 않으며, 만약 Pod에 영속적인 데이터 저장을 원한다면 볼륨 생성이 필요
* 클러스터 환경에서 데이터 액세스에 대한 관리는 컴퓨팅에 대한 자원 관리보다 어려운 부분이지만 Kubernetes는 이를 위해 다양한 옵션을 지원

#### Node의 디렉토리에 매핑되는 Volume 사용
* HostPath를 사용하여 데이터를 Node에 물리적으로 저장
* Node간의 데이터를 공유하기에는 적합하지 않은 구성
* Pod에 보안상의 취약점이 있는 경우 Node까지 액세스 가능
  * 액세스 가능한 경로에서 루트 경로로 접근하는 것을 막기 위해 하위 경로에만 접근 제한하는 설정이 가능

> 보편적인 Kubernetes 클러스터 환경에서 사용하기엔 적합하지 않은 설정 

#### PersistentVolume을 사용 (정적 프로비저닝)
* PersistentVolume을 사용하여 클러스터에 스토리지를 추상화
* Pod는 PersistentVolume에 액세스하기 위해 PersistentVolumeClaim (PVC)을 사용해서 요청
  * PVC에는 액세스 모드, 스토리지 크기, 스토리지 클래스를 정의
* Kubernetes는 Claim의 요구사항에 일치하는 기존 PV를 찾으려고하며, 항목이 없는 경우 PVC를 PV에 바인딩
  * 1:1 링크로 인해 PV가 바인딩되면, 다른 PVC에서는 사용 불가
* Pod는 바인딩되지 않은 PVC를 참조하려하는 경우, PVC가 바인딩될때까지 Pending 상태로 유지

#### PersistentVolume을 사용 (동적 프로비저닝)
* PVC를 작성하면, 이를 지원하는 PV가 클러스터의 요청시 작성
* PV를 만들지 않고 PVC를 클러스터에 배포할 수 있는데, 이 경우 Kubernetes가 구동되는 플랫폼에 따라 내부 동작이 다름
  * 예) Docker Desktop의 경우 동적 프로비저닝으로 생성된 PV에 대해 기본 스토리지 클래스의 HostPath 볼륨을 사용



### 추가 Reference
* [볼륨](https://kubernetes.io/ko/docs/concepts/storage/volumes/)


</p>
</details>

## 06

### memo
<details><summary>CLICK ME</summary>
<p>


Kubernetes에서 애플리케이션 확장을 위해서는 Pod를 여러개 실행하면 된다. 
* 컴퓨팅 계층에서 네트워크 및 스토리지를 추상화하기 때문에, 동일한 앱의 복제본인 Pod를 여러개 실행하고 추상화된 계층에 연결
* 복제본인 Pod를 호출함으로써 다중 노드 클러스터에서는 여러 노드에 분산
* `ReplicaSet`을 통해 Pod의 복제본 값을 설정, 보통 `Deplyment` 컨트롤러의 `replicas` 값을 설정하는 방법으로 활용
* Kubernetes 클러스터 내에 들어오는 트래픽 처리를 위해 `LoadBalancer` 서비스를 사용 (엄밀히 따지면 Reverse Proxy)


</p>
</details>

## 07

### memo
<details><summary>CLICK ME</summary>
<p>


Kubernetes는 하나의 Pod 내에 여러 Container를 생성할 수 있다.
* Pod 내의 컨테이너들은 동일한 Pod의 IP 주소를 공유
* Pod 내의 컨테이너들은 컨테이너 내에 자체 파일 시스템을 가질 수 있고, Pod에서 볼륨을 마운트하여 데이터를 공유

컨테이너를 배포하는 형태는 다음과 같은 형태들이 있다.
* 사이드카 패턴: 애플리케이션의 주기능을 담당하는 메인 컨테이너와 메인 컨테이너를 보조하는 서브 컨테이너 구성
* 초기화 패턴: Init 컨테이너를 통해, 메인 컨테이너 실행시 필요한 정보들을 초기화 할 수 있도록 구성
* 앰배서더(ambassador) 패턴: 애플리케이션에서 네트워크를 제어할 수 있도록 구성

</p>
</details>

## 08

### memo
<details><summary>CLICK ME</summary>
<p>


Kubernetes에서 데이터 집약적인 애플리케이션을 위해서는 StatefulSets, Jobs 및 CronJobs와 같은 컨트롤을 활용할 수 있다. 
* StatefulSets: 클러스터링 구성된 애플리케이션을 다루기 위해 활용
  * 고가용성을 위해 기본 인스턴스와 보조 인스턴스로 구성된 경우, 보조 인스턴스를 시작하기 위한 논리적인 순서를 설계 가능 (초기화 패턴 활용)
  * 인스턴스를 0 ~ n까지 순서대로 생성하며, 축소해야하는 경우 역순으로 제거
  * `volumeClamTemplates`를 활용해 스토리지 계층을 추상화하여 Pod가 교체 될 때 Pod와 PVC 사이의 링크를 유지
* Jobs & CronJobs: 데이터 백업 및 조정을 위해 활용
  * `restartPolicy`를 활용해 실패에 대한 응답으로 작업의 동작을 제어
  * 동일한 다수의 Pod를 병렬로 실행하는 워크로드를 수행
  * 데이터베이스 백업 프로세스를 정기적으로 수행하는 작업


</p>
</details>

## 09

### memo
<details><summary>CLICK ME</summary>
<p>


Kubernetes에서 애플리케이션을 배포하는 경우, 애플리케이션의 업데이트를 안전하게 수행하고, 잘못된 경우 업데이트를 일시 중지하고 롤백할 수 있는 매커니즘이 있다.
* 버전이 다른 애플리케이션 간의 배포는 서로 다른 ReplicaSet으로 격리
* Rollout 기록은 단순하기 때문에 추적을 위해 버전 정보(Commit Id 등)을 추가하는것이 유용
* Hot Reload 방식으로 배포에 대한 변경을 하지 않고 ConifgMap을 이용해 애플리케이션의 설정 변경 가능
  * 이 경우 롤백 대상을 알 수 없음
  * vs. 롤백 활성화를 위해 설정 개체를 변경 불가능(immutable)하다고 가정하고, 설정이 변경되는 경우 새 설정 개체를 생성하고 해당 개체를 참조하는 배포 업데이트를 함께 릴리즈 하는 방안 존재 (경우에 따라 각각 장단점 존재)
* Rolling 업데이트의 설정 (Rolling Update 배포 전략의 경우 새 애플리케이션과 이전 버전 애플리케이션이 동시에 존재할 수 있기 때문에 충돌 방지를 위해 설정이 중요) 
  * `maxUnavailable`: 이전 ReplicaSet을 축소
  * `maxSurge`: 새로운 ReplicaSet을 확장
  * `minReadySeconds`: 배포가 대기하는 지연시간 (모든 배포에 적용하는 것을 권장)
  * `progressDeadlineSeconds`: 배포 업데이트가 진행 실패로 간주되기 전에 실행할 수 있는 시간
* DaemonSet과 StatefulSet의 경우에도 RollingUpdate를 기본값으로 갖고, OnDelete 값을 활용 할수도 있음
  * `OnDelete`: 업데이트 되는 시기를 세부적으로 제어 
* 블루-그린 배포: 이전 버전과 새 버전의 애플리케이션이 배포되어 있지만, 서비스의 레이블 선택기를 업데이트하여 하나의 버전만 선택해 운영 가능한 배포 전략
  * 두 버전의 에플리케이션을 구동하기 위한 리소스가 필요하며, 이 경우 앱의 출시 기록을 자체적으로 보존하지 않음
  * 장기적으로 Rolling Update 전략을 취해야 하지만, 초기 도입시에 유용하게 활용 가능한 전략


</p>
</details>

## 10

### memo
<details><summary>CLICK ME</summary>
<p>


Helm은 Kubernetes YAML 파일 세트를 하나의 아티팩으로 관리할 수 있도록 해주며, 이를 통해 누구나 YAML 파일 세트에 액세스할 수 있다면, 단일 Helm 명령으로 앱을 설치할 수 있다.
* `chart`: Helm의 애플리케이션 패키지
  * Kubernetes YAML 매니페스트를 포함
* `repository`: chart를 게시하는 공간
* `release`: chart를 설치하는 동작 

Helm chart 파일 구조
* `chart.yaml` 파일: 이름과 버전을 포함한 차트 메타데이터를 지정
* `values.yaml` 파일: 매개변수의 기본값 설정
* `templates` 폴더: 템플릿화된 Kubernetes 매니페스트를 포함

릴리즈 단계
1. 차트를 zip 아카이브로 패키징
2. 아카이브를 서버에 업로드
3. 레포지토리 인덱스를 업데이트하여 새 차트를 추가

특이 사항
* Helm을 사용하면 모든 작업에 대한 정교한 템플릿을 생성할 수 있다.
* Helm을 통해 동일한 YAML 세트를 여러번 배포하는 경우, Kubernetes는 동일한 리소스만 업데이트한다. 
* Helm의 워크플로우는 kubectl 워크플로우와 호환되지 않는다. 
* Helm chart는 레포지토리에 게시하기 전에 패키징해야 한다.


</p>
</details>

## 11

### memo
<details><summary>CLICK ME</summary>
<p>


Kubernetes를 이용해 Plaform-as-a-Service (PaaS)로 활용하면, CI/CD 서비스를 호스팅하는 모든 테스트 환경에 단일 클러스터를 실행하여 컨테이너 실행에 대한 복잡한 세부 정보를 처리할 수 있다.

  
</p>
</details>
