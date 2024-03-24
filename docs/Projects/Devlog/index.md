---
hide:
title: 단축키 설정
---

[mkdocs reference](https://squidfunk.github.io/mkdocs-material/reference/)를 보면 아주 많은 formatting 기능이 소개 된다. 당장 사용 가능하게 out-of-box로 제공되기도 하고, `/mkdocs.yml`에서 한줄 한줄 추가해서 기능을 확장할 수도 있다.

나는 최대한 가볍게 사용하려고 했는데, 그래도 ==highlight== 랑 ~~취소선~~ 정도는 유용하겠다.

더 쉽게 활용하기 위해 확장자가 `.md`일 경우 활성화되는 단축키로 지정해보자.

## neovim keymap

마침 사용중인 `markdowny.nvim`이라는 플러그인에서 거의 비슷한 기능을 제공한다. 이 플러그인에 몇가지 추가해서 임시로 사용한다.

```lua
-- antonk52/markdowny.nvim

function M.mark()
  inline_surround('==', '==')
end

function M.tilde()
  inline_surround('~~', '~~')
end

vim.keymap.set('v', '<C-h>', ":lua require('markdowny').mark()<cr>")
vim.keymap.set('v', '<C-d>', ":lua require('markdowny').tilde()<cr>")
```

## 덧

플러그인 리포지토리에 [이슈](https://github.com/antonk52/markdowny.nvim/issues/11)도 남겼다. 기능을 추가해주기만 해도 좋고, 어쩌면 opensource에 PR을 남겨볼 기회도 되겠다.
