---
title: 'sysz: interactive ui for systemctl'
date: 2024-04-16
---

정확히는 TUI는 아니겠다. 단지 fzf를 활용해서 systemctl를 더욱 interactive하게 사용하는 스크립트 정도라고 할 수 있다. 제작자도 오직 shell script로만 제작했다고 강조한다.

매번 `systemctl status`를 치면서 번거로웠고, 마땅한 도구가 안보여서 fzf preview를 활용해서 직접 만들까 했는데, 오늘 보니 멀쩡한게 있다.

## sysz

A fzf terminal UI for systemctl

### Features

_VERSION: 1.4.3_

- See and filter both system and user units simultaneously.
- Supports all unit types.
- Units ordered by service, timer, socket, and the rest.
- Runs sudo automatically and only if necessary.
- Filter units by state using ctrl-s or the --state option.
- Run daemon-reload with ctrl-r.
- Has short versions of systemctl commands to reduce typing.
- Runs status after other commands (start, stop, restart, etc).
- Select multiple units, states, and commands using TAB.
- Only prompts commands based on current state (e.g. show "start" only if the unit is inactive).

## reference

- [github](https://github.com/joehillen/sysz)
