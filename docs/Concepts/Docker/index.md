---
hide:
title: "도커의 이해"
date: 2024-03-27
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

**보안을 위한 원천 차단**

- local-network <==> docker-network
- docker-network <==> another-docker-network

#### ????

1. 어떻게 연결(통신)하고 분리시킬 것인가?

### 볼륨

**데이터의 영속성을 위하여**

- local => container
- container => local
- container => container

#### ???

1. 마운트와의 차이점이 뭐야?

### 이미지

**버전 관리, 아카이빙**

- 버전관리
- 덮어쓰기

#### ????

### 컨테이너

### 환경변수, secret

### 권한

### 로깅
