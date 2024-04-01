---
hide:
title: "도커의 구성요소"
date: 2024-03-27
update: 2024-03-30
---

> 차근 차근 완성시켜가는 문서입니다.
> 개인적인 개념 지도입니다. 공부는 공식 문서로!

## 도커의 구성

- 네트워크
- 볼륨
- 이미지
- 컨테이너
- 환경변수, secret
- 권한
- 로깅

### 네트워크

보안을 위한 원천 차단

- local-network <==> docker-network
- docker-network <==> another-docker-network

### 볼륨

데이터의 영속성을 위하여

- local => container
- container => local
- container => container

### 이미지

버전 관리, 아카이빙

- 버전관리
- 덮어쓰기

### 컨테이너

컨테이너의 상태에 따른 활용

- alive
  - running
  - pause
- dead
- broken

### 환경변수, secret

잘 모른다. 그냥 `.gitignore` 리스트에 넣어두고 원시적으로 관리하는 정도.

### 권한

하나도 신경 안쓰고 있었다.

불편한 거라면 volume으로 설정한 디렉토리의 파일을 직접 손대려고 하면 권한 문제가 발생하는점이다.

### 로깅

하나도 신경 안쓰고 있었다. 뭐가 잘 안되면 `docker logs` 명령으로 살펴보기나 했지.

배포 환경에도 도커를 활용한다면 이렇게 무책임해서는 안되겠다.
