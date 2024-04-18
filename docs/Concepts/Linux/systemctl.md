---
title: "about systemd"
date: 2024-04-16
---

배우기보단 실사용을 먼저했다. 구글링으로 얻은 커맨드를 실행하다보니 패턴을 발견하는 정도.

`sysz`라는 관리도구를 사용하기 시작한 지금부터는 알고 써야겠다.

## What is "systemd"

- init system
- 모든 (background)service를 관리

### init의 세대 교체

`init`은 부팅 후 가장 먼저 실행되는 PID 1번 프로스세스였다. 이것이 `systemd`로 대체된 것이다.

`init`은 쉘 스크립트로 작성된 파일을 실행하는 방식이었는데, `systemd`는 이를 `unit`라 부르는 요소로 바꿔 속도와 가독성을 개선했다.

`systemd`는 이뿐만 아니라 다른 기능들도 대체했다.

## Types of "unit"

- unit은 systemd가 모든것을 시작하고 관리하는데 사용하는 요소
- 관리 대상들을 `<service name>.<unit type>`으로 지칭
- 동일한 naming을 따르는 설정 파일을 사용

  |   unit    | 예시                              | 기능                           |
  | :-------: | :-------------------------------- | :----------------------------- |
  |  service  | atd.service                       | 데몬의 시작, 종료, 재시작 담당 |
  |   timer   |                                   |                                |
  |  socket   | dbus.socket                       |                                |
  |  device   | dev-sda.device                    |                                |
  |   mount   | boot.mount                        |                                |
  | automount | proc-sys-fs-binfmt_misc.automount |                                |

실사용시 주로 serives를 다루게 되겠지만, 이 밖에도 다양한 종류의 unit이 있다는것을 알아두기를 권한다.

## Where are unit files?

아래의 다양한 위치에 있다. 각각이 상이한 목적을 가진다.

**특히 1>2>3 번호순으로 높은 priority를 가진다.** unit file은 말하자면 설정파일이기 때문에 덮어 씌워진다는 뜻이다.

1. `/etc/systemd/system/`
   - 가장 자주 방문할 위치.
2. `/run/systemd/system/`
   - systemd가 전체 시스템을 관리하는 와중에 생기는 임시파일 따위를 저장하는 곳. 사람이 관여할 일이 없다고 보면 된다.
3. `/lib/systemd/system/`
   - application이 설치될 때 필요하면 여기에 만들어진다. 낮은 우선순위를 갖는건 당연하다. 내가 시스템의 주인이니까.

## How is "unit file" look alike?

우리는 기계가 아니니까, 모든 종류의 unit을 다룰수는 없다. 다만 대략 이렇게 생겼다는것을 살펴보자.

예시로 apatch web server를 설치하면 httpd.service 유닛이 생성된 것을 볼 수 있을 것이다.

열어보면 3개의 section이 있다. 각각에는 필수/비필수 field가 있다. 이것들은 배포판마다 다르기도 하다.

```unit file
[Unit]
Description=Apache Web Server
After=network.target remote-fs.target nss-lookup.target ; prerequisite before this unit

[Service]
Type=simple ; unit의 타입. 모두 알 필요 없다.
ExecStart=/usr/bin/httpd -k start -DFOREGROUND ; systemctl 따위로 start 명령시 수행할 것
ExecStop=/usr/bin/httpd -k graceful-stop
ExecReload=/usr/bin/httpd -k graceful
PrivateTmp=true
LimitNOFILE=infinity
KillMode=mixed

[Install]
WantedBy=multi-user.target ; 리눅스 시스템에는 run level이라는게 있는데, 이것이 unit에서 특정된 단계까지 진행된 이후에 실행되라는 것. 이것도 일종의 prerequisite이라 볼 수 있겠다.
```

## How to edit this?

### edit

`systemctl edit <service>`  
path는 굳이 줄 필요 없다.

unit 파일의 문법에 맞게 override 할 부분만 작성해주면, `/etc/systemd/system/<service>.d/override.conf`처럼 최상위 파일이 생성된다.

> `--full` flag를 추가하면 완전히 대체할 파일을 작성할 수 있다.(원본 복사해서 시작)
>
> 패키지 업데이트 등에도 변함없이 나만의 설정을 유지해야한다면 이것이 좋은 대안이 될 것이다.

### delete

변경 내용을 되돌리는것도 간단하다. 이 파일을 삭제하면 된다.

### reload

`systemctl daemon-reload [ <service> ]`

물론 실행중인 서비스가 종료되지는 않는다. 단지 unit 파일에 변경사항이 있는지 확인하고 load하는것 뿐이다.

> 그러나 돌다리도 두들겨 보고 건너자.

## self-QnA

- **Loaded, Active**가 나뉘어진 이유는 뭐야?

  > **Loaded**: systemd가 해당 서비스의 unit 파일을 읽고 파싱해서 메모리에 로드했다는 뜻.

- **Loaded**의 괄호 내부에 표현되는 "상태"들의 종류

  아래의 요소들 외에도 어쩌구 저쩌구 많다만, 일단 이거라도 한번 읽어보자.

  > **enabled**: 자동시작 O  
  > **disabled**: 자동시작 X

  > **static**: 기타 유닛에 의해서 관리되는 서비스. 그러니 (이름처럼)자동시작 걸고 자시고 필요가 없다. 때가 되면 분연히 떨치고 일어난다.

  > **transient**:  
  > 기타 유닛이 실행될 때(runtime) 필요해서 생겨나고 또 사라지는 놈. 위에서 공부한 `/run/systemd/system/`에 unit 파일이 생기고 삭제 된다.
  >
  > 내 시스템을 조회해보니 docker container들과 kubernetes pod들이 이런 상태를 가진다. 헌데 `/run/systemd/system/`에는 없다. 모든 서비스의 unit 파일이 해당 위치에서 보이는건 아니란 뜻이다.

  > **generated**: systemd가 직접 관리하는 요소는 아니지만(_unit 파일이 없다._), 기타 시스템 구성요소로부터 service로 실행될 놈들이다.
  >
  > 역시나 `/run/systemd/system/`에 unit 파일이 임시로 생성되고 삭제된다.
  >
  > 내 시스템을 살펴보면 몇가지 mount point가 이 상태를 가지고, 이외에는 autostart 되는 실행파일들이다.

  > **preset**: package manager가 app을 설치할 때 설정된 내용을 기록한 것. 역시 리눅스!!

- init을 대체한다는데, 그럼 최초에 실행될 service 또는 service list는?

  > `systemctl get-default`
  >
  > 내 경우엔 **graphical.target**이 조회되는데, 이놈을 뜯어보면 또 다른 **multi-user.target**을 실행시킨다. 이것들은 공부를 좀 더 해봐도 좋을 것 같다.

  - **graphical.target**

    > ...

  - **multi-user.target**

    > ...

- `Unit <unit name> could not be found.`라고 나오는 것은 뭐야? 어떻게 대처해?

  > sysz와 systemctl의 리스트 결과가 매우 다르다. 개수만 봐도 5배이상... 뭘까? sysz를 좀 더 뜯어봐야겠다. 봐도 모르겠으면 레딧에 물어보자.

- `<unit name>.service`가 아니라 `<unit name>@.service`의 정체는 뭐야?

  >

## reference

- youtube: [[따라學 IT] 04. systemd - 이론](https://www.youtube.com/watch?v=vg8bcRlNXB8&t=678s)
- youtube: [Systemd Deep-Dive: A Complete, Easy to Understand Guide for Everyone](https://www.youtube.com/watch?v=Kzpm-rGAXos)
