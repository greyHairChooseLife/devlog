---
hide:
title: "kubernetes alias"
date: 2024-04-07
update:
---

솔직히 이정도는 alias로 만들기 우습다. 이정도는 좀 숨쉬듯이 쓰고 싶다.

## 모든 파일에 명령

```sh
for file in *.yaml; do kubectl <apply> -f $file; done
```
