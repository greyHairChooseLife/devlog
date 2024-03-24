# 블로그 대문

안녕하세요. 저의 블로그에 오신 것을 환영합니다.

(상연아, 너도 환영해)

## 가슴에 새기고 살아갈 말들

- **재행무상**
- **제법무아**
- **일체개고**

## new keymaps

- CLI: custom fzf

```bash

  Hello, fzf!

        ff         fzf_file_current
        ff.        fzf_file_current_hidden
        ffr        fzf_file_recursive
        ffr.
        ff.r       fzf_file_recursive_hidden

        fl         fzf_CD_current_(relative)
        fl.        fzf_CD_current_(relative)_hidden
        flr        fzf_CD_current_recursive
        flr.
        fl.r       fzf_CD_current_recursive_hidden
        flh        fzf_CD_home
        flh.
        fl.h       fzf_CD_home_hidden

--bind  ctrl-x     clear-query
--bind  ctrl-j     jump
--bind  ctrl-t     last
--bind  ctrl-b     first
--bind  ctrl-u     half-page-up
--bind  ctrl-d     half-page-down
--bind  alt-p      preview-half-page-up
--bind  alt-n      preview-half-page-down
```

- NVIM: custom keymaps

```vim
<Leader><Leader>s => auto-session save
,.S               => load list of sessions
<C-d> =>
```

- Package Manager: custom keymaps

preview를 활용해서 패키지 정보를 자세히 확인 가능하다. fzf의 세계는 넓다...

```bash
yayinstall
yayremove
pacinstall
pacremove
```
