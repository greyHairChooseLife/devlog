---
hide:
title: "쿠버네티스의 이해"
date: 2024-04-01
update:
---

> (개발 단계부터 이미지 생성까지는 도커 클라이언트를 활용하고)  
> 컨테이너 관련 작업이 배포 및 운영 단계로 넘어가기 시작하면 쿠버네티스를 사용할 때다.

## 목적

컨테이너화된 애플리케이션의 배포, 스케일링, 상태관리를 자동화

## 주요 구성요소

### 마스터 노드

- API 서버
- 스케줄러
- 컨트롤러 매니저
- etcd

### 워커 노드

- kubelet
- kube-proxy
- 컨테이너 런타임

## Kubernetes Workload

### Pod

1. `docker run` 으로 컨테이너를 생성/실행한 것 처럼 `kubectl run` 명령으로 pod를 생성/실행할 수 있다.

   다만 쿠버네티스 생태계에서 pod처럼 작은 단위를 직접 관리하지는 않는것이 보통이다. 대신 Deployment나 StatefulSet 같은 리소스를 사용한다.

2. pod는 하나 이상의 컨테이너로 구성된다. pod 자체의 상태를 조회할 수도 있고, pod 내부의 특정 컨테이너를 조회할 수도 있다.

   ```sh
   kubectl get pod
   kubectl get pod -o wide

   # 주로 Events부분을 확인한다. Pod의 생성, 시작, 종료 등의 이벤트를 순서대로 확인할 수 있다.
   kubectl describe pod/<podname>

   kubectl logs pod
   kubectl logs -f pod # log streaming, --follow

   kubectl exec -it <podname> -- sh
   kubectl exec -it <podname> -c <container name> -- sh
   ```

### ReplicaSet

- pod의 템플릿을 정의하고, 원하는 수의 pod 인스턴스를 유지하도록 한다.

  ```sh
    spec:
        replicas: <pod 복제본 수량>,
        selector: <pod 선택자, 무엇을 관리할 것인지 알아볼 수 있도록 지정한다.>,
        template: <복제 생성할 pod 템플릿>
  ```

### Deployment

- 가장 널리 사용되는 오브젝트다.
- ReplicaSet을 이용하여 Pod를 관리한다. Pod의 업데이트, 롤백, 스케일링 할 수 있다.

## reference

- [Kubernetes Explained in 6 Minutes | k8s Architecture](https://www.youtube.com/watch?v=TlHvYWVUZyc)
- [쿠버네티스 아키텍쳐-유투브](https://www.youtube.com/watch?v=-gIyfII5eak)
- [쿠버네티스 초급 안내서](https://subicura.com/k8s/guide/pod.html#%E1%84%88%E1%85%A1%E1%84%85%E1%85%B3%E1%84%80%E1%85%A6-pod-%E1%84%86%E1%85%A1%E1%86%AB%E1%84%83%E1%85%B3%E1%86%AF%E1%84%80%E1%85%B5)
