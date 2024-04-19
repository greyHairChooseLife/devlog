---
hide:
title: '컨테이너를 다루는 도구들'
date: 2024-04-01
update:
---

## docker

- [lazydocker](https://github.com/jesseduffield/lazydocker)

  docker client를 머금은 TUI 패키지다. lazygit을 만든 사람이 만들어서, 둘 다 비슷하고 또 믿을만 하겠다.

  `docker`, `docker compose` 클라이언트의 커맨드(api)를 모두 사용할 수 있다. 사전에 정의해둔 attatch,
  detatch, logs 등 명령어를 단축키에 지정해서 간편하게 사용하는 방식이다.

  docker objects _(service, container, image, volume, network)_ 를 각각의 패널에 나눠서 보여주고, 각각의
  패널에서 커맨드를 실행할 수 있다. 확실히 시각적으로 맥락을 파악하기 좋다.

## kubernetes
