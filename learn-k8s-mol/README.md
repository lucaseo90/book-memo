# Learn K8s(Kubernetes) MOL(in a Month of Lunches)

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
