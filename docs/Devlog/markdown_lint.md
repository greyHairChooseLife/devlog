---
hide:
title: "마크다운 문법 익히기"
date: 2024-04-01
update:
---

> 아마도 마크다운이 평생가는 문서 양식이 될 것 같다. 그렇다면 글로벌 기준으로 문법을 익히는 것이 좋겠다.

## 린트 오류

### MD033/no-inline-html

- error message

```
MD033/no-inline-html: Inline HTML [Element: br] (markdownlint)
```

- occasion

```markdown
> 가나다라
> <br>마바사아

<!-- 단순 줄바꿈을 하고싶었다. 아래 처럼 시도하면 아예 한 줄이 추가된다. -->

> 가나다라
>
> 마바사아
```

- solution

```markdown
> 가나다라 (여기에 공백을 2개 추가한다.)
> 마바사아
```
