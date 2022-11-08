# Imitated-seed
더시드 엔진 (구 프론트엔드 기준) 모방 프로젝트.

테스트 서버 - https://jdh5968.pe.kr (`flight` 브랜치)

나무픽스와 거의 호환된다.

## 경고
**이 레포는 실사를 위해 생성한 포크다. PR로 깽판 치면 잠궈버릴 거니 유의 바람.**

원본 보고 싶으면 [여기](https://github.com/gdl-blue/imitated-seed-2)로.

마개조 일지는 [위키](https://wiki.jdh5968.pe.kr/w/개발일지:개발일지)에도 씨부려 놨지만, 간단하게 [여기](https://github.com/JeonDohyeon/imitated-seed/wiki/패치-일람)에서도 볼 수 있다.

## 기초 사용 방법
- **만약 config.json에서 `use_external_js`과 `use_external_css`이 true이면 아래 단계는 생략해도 된다.** 스킨만 추가하면 된다.
  - css, js 디렉토리를 만든다.
    - [theseed.js](https://theseed.io/js/theseed.js), [jquery-2.1.4.min.js](https://theseed.io/js/jquery-2.1.4.min.js), [jquery-1.11.3.min.js](https://theseed.io/js/jquery-1.11.3.min.js), [intersection-observer.js](https://theseed.io/js/intersection-observer.js), [dateformatter.js](https://theseed.io/js/dateformatter.js)를 각각 다운로드받아 js 디렉토리에 복사한다.
    - [wiki.css](https://theseed.io/css/wiki.css), [katex.min.css](https://theseed.io/css/katex.min.css), [diffview.css](https://theseed.io/css/diffview.css)를 각각 다운로드받아 css 디렉토리에 복사한다.
- skins 디렉토리를 만든다.
  - [buma](https://github.com/LiteHell/theseed-skin-buma/tree/d77eef50a77007da391c5082b4b94818db372417), [liberty](https://github.com/namuwiki/theseed-skin-liberty/tree/153cf78f70206643ec42e856aff8280dc21eb2c0) 등 원하는 스킨을 내려받고 skins 디렉토리에 스킨 이름으로 하위디렉토리를 만들어 복사한다.
- `npm i`를 실행한다.
- `node server`를 실행한다.

### 잡소리
- css, js 관련
  - ps1 파일로 스크립트화했다. 반드시 css 폴더 만들고 실행할 것. 지가 알아서 다 다운받아준다.
  - 스킨은 직접 다운받아라. 제발.
  - 이 ps1 파일과 대응되는 bat 파일은 없다. wget 쓰는데 있을 리가. 대신에 sh 파일 만들었으면 issue에 올려주면 추가해보겠다.
- 스킨
  - 사실, skins 디렉토리 안에 원하는 스킨 이름 디렉토리를 만들어서 거기다 포크를 때려도 된다.  
  아니면, skins 아래에 `git submodule add <url> [relative-dir]` 써도 된다.
    - 구현체에 따라서 파일이 다 올라오는 경우도 있고 자동으로 submodule화되는 경우가 있어서 현재는 submodule로 통합.
  - 난 지금 자체 포크 개조판 쓴다. 자세한 건 내 레포 목록 확인.

## 추가 도구
- undelete-thread.js: 삭제된 토론 복구
- namuwiki-importer.js: 나무위키 데이타베이스 덤프 가져오기

## config.json
- config.json 수정으로 숨겨진 설정을 제어할 수 있다.
  - `disable_email`: (기본값 false) 전자우편 인증을 끈다.
  - `disable_login_history`: (기본값 false) 로그인 내역을 기록하지 않게 한다.
  - `use_external_js`: (기본값 false) theseed.js, jQuery 등을 [theseed.io](https://theseed.io)에서 불러온다.
  - `use_external_css`: (기본값 false) wiki.css 등을 [theseed.io](https://theseed.io)에서 불러온다.
  - `allow_account_deletion`: (기본값 false) 계정 탈퇴를 허용한다.
  - `allow_account_rename`: (기본값 false) 닉네임 변경을 허용한다.
  - `search_host`: (기본값 "127.5.5.5") 검색 서버 호스트 주소
  - `search_port`: (기본값 25005) 검색 서버 포트
  - `search_autostart`: (기본값 false) 같은 디렉토리에 검색 서버 프로그램(search.js)이 있을 경우 위키 서버 시작 시 검색 서버를 같이 시작시킨다.
  - `no_username_format`: (기본값 false) 한글, 공백 등의 특수문자를 사용자 이름으로 쓸 수 있게 하고 길이 제한을 없앤다.
  - `owners`: (기본값 \[\]) /admin/config에 접속할 수 있는 사용자 이름 배열
  - `reserved_usernames`: (기본값 \["namubot"\]) 이 배열 안에 있는 닉네임으로 계정을 만들 수 없다.
  - `theseed_version`: (기본값 "4.12.0") [the seed 판올림 기록](https://namu.wiki/w/the%20seed/%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8#toc)을 참고하여, 모방할 the seed 엔진의 버전을 지정한다.
    - 형식 주의! 4.4(X), "4.4"(X), 4.4.1(X), "4.4.1"(O) 문자열 x.y.z 형식으로.
    - 예를 들어, "4.4.2"로 할 경우, v4.4.3에 추가된 쓰레드 주제/문서 변경 기능을 사용할 수 없고,  
      "4.18.0"으로 할 경우 IPACL과 사용자 차단 기능이 비활성화되고 ACLGroup가 활성화되며 ACL에서 이름공간ACL 실행 action를 사용할 수 있다.
  - `replicate_theseed_license`: (기본값 false) 라이선스 페이지를 더시드 엔진처럼 띄운다. 가급적이면 쓰지 않는 것을 권장한다.
  - `namuwiki_exclusive`: (기본값 false) 나무위키 전용 기능(경고 ACL 그룹, 문서 이전 판 경고 등)을 활성화한다.
  - `enable_captcha`: (기본값 false) 보안문자를 쓰게 한다.
  - `block_ip`: (기본값 []) 접속을 차단할 IP를 지정한다. CIDR는 지원하지 않는다.
  - [추가] `get_long_license`: (기본값 false) 라이선스 페이지를 더시드 엔진의 것을 기반으로 imitated-seed에 맞춰 변형한 "긴 라이센스"로 띄운다.

### 잡소리
- 검색 서버 설정은 안 건드리는 게 정신건강에 이롭다.  
근데 켜두는 게 좋다.

## misc.json
- config.json이 아닌 또다른 설정 파일로, 내부 설정을 제어하지만 config와 달리 코드와는 크게 관련 없는 부분을 수정한다.  
얘만의 특징으로, 처음 시작 시 기본값을 모두 적어준다.
  - `wiki_ver`: (기본값 `20220917`) 체크아웃 중인 master 브랜치의 최종 수정일을 의도했다.  
  맘대로 버전 지정 해도 상관없다. 그러라고 만든 필드다.  
  `config.get_long_license`가 true여야 표시된다.
  - `edited`
    + `is_edited`: (기본값: false) license 표시 중 수정된 판인지를 표시하기 위해 넣어두었다.  
    `config.get_long_license`가 true여야 작동한다. 또, `edited.date`가 ''(빈 값)이면 false로 조정된다.
      * false로 조정되더라도 파일에선 true로 표시될 수 있다.
    + `author`: (기본값: []) 이 수정판을 누가누가 수정했는지를 표시한다.  
    `config.get_long_license`와 `edited.is_edited`가 모두 true고, `edited.date`가 ''(빈 값)이 아니어야 표시된다.
    + `date`: (기본값: '') 이 수정판의 최종 수정일을 표시한다.  
    `config.get_long_license`와 `edited.is_edited`가 모두 true여야 표시된다.

## 라이선스
자유롭게 쓰기 바란다. (렌더러는 개조 시 소스 코드 공개해주었으면 좋겠음. 그리고 포크판을 특허출원 하지 마라.)

### 스킨 라이선스
스킨 라이선스는 각 스킨의 루트 디렉토리에 있다. 항상 자체 포크판 정도만 쓰니 내 레포 목록 봐도 좋다.

## 더 시드와 다른 것들
- 엔진에서 백엔드와 프론트엔드를 모두 처리한다. (오픈나무에서 영향 받음)
- 밀리초 유닉스 시간을 사용한다.
- /notify/thread 라우트가 제대로 되어있지 않다.

## 알려진 문제점
issues로.
