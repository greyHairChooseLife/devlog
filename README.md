# 김상연의 개발 블로그

markdown으로만 작성하는 개발 블로그를 운영하기로 했다.

최초에는 **종립**님의 블로그를 통해 영감을 받았고, [mkdocs](https://github.com/mkdocs/mkdocs)라는 멋진
doc-generator를 발견한 덕에 쉽게 시작한다.

## 1. 배포

> write & commit & push & all done!

깃헙 페이지를 통해 배포한다. static 사이트인 만큼 매번 새로 빌드해야 한다.

정말 친절하게도 mkdocs에서 빌드, 배포까지 자동화 할 수 있는 github action을 제공한다. main 또는 master
브랜치에 push하면 알아서 빌드, 배포 된다.

## 2. 어디에서나 노트를 이어서 작성하기

1. git clone

2. `docs/` 위치에 작성

```tree
.
├── docs
├── cinder
├── mkdocs.yml
├── node_modules
├── package.json
├── pnpm-lock.yaml
└── README.md
```

## 3. CLI commands

### 3.1 테스트 서버 실행

`mkdocs serve`

### 3.2 새로운 노트 생성

`mkdocs new [note-name]`

## 4. Theme, 예제, Markdown parser

- [cinder theme](https://sourcefoundry.org/cinder/)
- [문서 작성 예제](https://sourcefoundry.org/cinder/specimen/)
- [markdown (parser) by JOHN GRUBER](https://daringfireball.net/projects/markdown/)
