---
hide:
title: "사용 사례"
date: 2024-04-01
update:
---

## best practices

### 1. take advantage of layer caching (as building image)

Dockerfile 작성 시 instructions의 순서를 적절히 배치하여 시간과 컴퓨팅 자원을 효율적으로 사용할 수 있다.

- _나쁜 예_

```Dockerfile
COPY src target
RUN npm install --production  # 소스 한글자만 바꿔도 npm install이 다시 실행된다.
```

- _좋은 예_

```Dockerfile
COPY packages.json packages-lock.json target
RUN npm install --production  # 패키지가 실제로 수정 될 때만 실행된다.
COPY src target

# .dockerignore에서 node_modules/를 제외시켜줘야 완성이다.
```

### 2. multi-stage builds

run-time에 필요한 환경과 build-time에 필요한 환경은 다를 수 있다. 각 단계에서 꼭 필요한 것만 갖다 쓰자.
