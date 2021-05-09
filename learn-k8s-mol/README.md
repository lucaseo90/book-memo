# Learn K8s(Kubernetes) MOL(in a Month of Lunches)

## 01

### memo
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

### practice
실습을 위한 Kubernetes 구성이 필요한데, macOS 기준으로 [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-mac) 설치 후 Dashboard에서 kubernetes를 활성화할 수 있다. 

```shell
$ kubectl get nodes
NAME             STATUS   ROLES    AGE   VERSION
docker-desktop   Ready    master   13d   v1.19.3
```

### 추가 Reference
1. [매니페스트 파일](https://ko.wikipedia.org/wiki/%EB%A7%A4%EB%8B%88%ED%8E%98%EC%8A%A4%ED%8A%B8_%ED%8C%8C%EC%9D%BC)
2. [쿠버네티스 컴포넌트 - etcd](https://kubernetes.io/ko/docs/concepts/overview/components/#etcd)
