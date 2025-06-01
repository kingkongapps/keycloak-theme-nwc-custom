## Keycloak UI 테마 수정하기
* Keycloak 의 공통화면(UI)들은 *.jar로 묶여 있다.
* 커스터마이징 할 수 있는 $KEYCLOAK_HOME/themes 디렉토리를 비어 있다.
* 따라서 공통화면(UI) 관련 *.jar을 압축을 풀고 themes 디렉토리에 복사해 놓고 수정하면 테마를 변경 할 수 있다.

> ### Keycloak UI 개발 환경
> * UI 개발언어 : Fremarker

### 공통UI JAR파일 복사하기
* Keycloak이 docker로 설치 된 경우, docker 버전 기준
```sh
cd
mkdir tmp
cd tmp

docker cp keycloak:/opt/keycloak/lib/lib/main/org.keycloak.keycloak-themes-26.1.3.jar .

jar xvf org*.jar
cd theme
tree -d
hosu@hosu-ubuntu:~/tmp/theme$ tree -d
.
├── base
│   ├── account
│   │   └── messages
│   ├── admin
│   │   └── messages
│   ├── email
│   │   ├── html
│   │   ├── messages
│   │   └── text
│   └── login
│       ├── messages
│       └── resources
│           └── js
├── keycloak
│   ├── common
│   │   └── resources
│   │       ├── img
│   │       └── lib
│   │           └── pficon
│   ├── email
│   ├── login
│   │   └── resources
│   │       ├── css
│   │       └── img
│   └── welcome
│       └── resources
│           └── css
└── keycloak.v2
    └── login
        └── resources
            ├── css
            ├── img
            └── js

## 이 디렉토리중에서 keycloak 을 $KEYCLOAK_HOME/themes 하위로 복사한다.
cp -r keycloak $KEYCLOAK_HOME/themes/keycloak-theme-nwc-custom
cd $KEYCLOAK_HOME/themes/keycloak-theme-nwc-custom
tree -d
hosu@hosu-ubuntu:~/keycloak-26.1.3/themes/keycloak-theme-nwc-custom$ tree -d
.
├── common
│   └── resources
│       ├── img
│       └── lib
│           └── pficon
├── email
├── login
│   └── resources
│       ├── css
│       └── img
└── welcome
    └── resources
        └── css
```

### UI 수정하기
* base/login/login.ftl을 위 디렉토리 구조도에서 login/ 밑으로 복사 후 수정한다.
* 수정 부분
  * backgroud image
  * 다국어 메시지 (아래 다국어 파일 복사 후 작업)
    * 등록 -> 회원가입
    * 비밀번호를 잊으셨나요? -> 비밀번호 재설정

### 다국어 message properties 수정하기
* base/login/messages 디렉토리를 login/messages로 복사한다.
* 복사후 각 나라 언어별 파일에서 메새지를 수정한다.
```
## 복사 후 디렉토리 구조
hosu@hosu-ubuntu:~/keycloak-26.1.3/themes/keycloak-theme-nwc-custom$ tree -d
.
├── common
│   └── resources
│       ├── img
│       └── lib
│           └── pficon
├── email
├── login
│   ├── messages    <------ 추가 됨
│   └── resources
│       ├── css
│       └── img
└── welcome
    └── resources
        └── css
```
