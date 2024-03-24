# 김상연의 개발 블로그

markdown으로만 작성하는 개발 블로그를 운영하기로 했다.

최초에는 **종립**님의 블로그를 통해 영감을 받았고, [mkdocs](https://squidfunk.github.io/mkdocs-material/)라는 멋진 프레임워크를 발견한 덕에 쉽게 시작한다.

## 배포와 글 쓰기

깃헙 페이지를 통해 배포한다. static 사이트인 만큼 매번 새로 빌드해야 한다.

정말 친절하게도 mkdocs에서 빌드, 배포까지 자동화 할 수 있는 github action을 제공한다. main 또는 master 브랜치에 push하면 알아서 빌드, 배포 된다.

docs 폴더에 md 파일을 작성하고 커밋, 푸시하면 끝이다.

## 어디에서나 노트를 이어서 작성하기

1. git clone

2. `docs/` 위치에 작성

```tree
.
├── docs
├── mkdocs.yml
└── README.md
```

## 새로운 노트 시작하기

mkdocs는 도커를 이용하여 설치하기 쉽게 제공된다. 아래 명령어를 통해 간단히 설치 가능하다.

> docker run --rm -it -v ${PWD}:/docs squidfunk/mkdocs-material new .
