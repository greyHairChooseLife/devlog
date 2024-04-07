---
hide:
title: 'Kubernetes networking'
date: 2024-04-07
update:
---

## Five essential things

- 동일한 `Pod`에 속한 `Containers` 간의 통신
- 동일한 `node`에 속한 `Pods` 간의 통신
- 서로 다른 `node`에 속한 `Pods` 간의 통신
- `Pod`와 `Service` 사이의 통신
- `DNS`의 작동원리(새로운 `endpoint`를 어떻게 발견할까?)

### 동일한 `Pod`에 속한 `Containers` 간의 통신

#### via

     - `localhost`
          - _어떤 `Pod`에 속한 컨테이너들은 `network namespace`_를 공유한다. 모든 Pod가 저마다의 namespace를 갖는 것.
     - `port`

#### `network namespace`란?

`network interfaces`와 `routing tables`의 모음. `namespace`를 통해 논리적으로 레이어를 구분하여 서로 충돌될 일이 없도록 한다.

참고로, Kubernetes의 모든 `Pod`에는 숨겨진 `container(aka pause container)`가 있다. 혹시나 모든 `Pod`가 죽어버렸을 때를 대비해 `namespace`가 open 상태를 유지하는 역할이다.

### 동일한 `node`에 속한 `Pods` 간의 통신

Kubernetes가 세팅한 환경에서 각 `Pods`는 고유한 `network namespace`를 소유하며, `ethernet device(aka eth0)`를 갖고 있다고 스스로 인식한다.

각 `Pod`의 `eth0`는 자신이 속한 `(worker)node`의 `(역시나 virtual)ethernet device`로 연결된다.

### 서로 다른 `node`에 속한 `Pods` 간의 통신

### `Pod`와 `Service` 사이의 통신

### `DNS`의 작동원리(새로운 `endpoint`를 어떻게 발견할까?)

## reference

[Kubernetes Networking Guide for Beginners](https://matthewpalmer.net/kubernetes-app-developer/articles/kubernetes-networking-guide-beginners.html)
