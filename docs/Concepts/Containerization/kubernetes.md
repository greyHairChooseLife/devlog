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

## 구성요소

### 마스터 노드

- API 서버
- 스케줄러
- 컨트롤러 매니저
- etcd

### 워커 노드

- kubelet
- kube-proxy
- 컨테이너 런타임

## reference

- [Kubernetes Explained in 6 Minutes | k8s Architecture](https://www.youtube.com/watch?v=TlHvYWVUZyc)
