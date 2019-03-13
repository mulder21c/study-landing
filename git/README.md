# Git CLI<sup id="cli"><a href="#foot-cli">[1]</a></sup> for Beginners

[Git CLI for Beginners Repository](https://github.com/mulder21c/git-study) &mdash; 스터디 참여자만 접근 가능합니다.

## 학습 목표

- Git에 대한 개념 잡기
- GUI 툴<sup id="gui"><a href="#foot-gui">[2]</a></sup>에 의존하지 않고 명령어 기반으로 Git 사용
- Terminal에서 바로 Git을 사용할 수 있는 기본 지식 함양

## 학습 대상

- 버전 관리 자체가 뭔지 모르는 이
- Git을 GUI로만 사용해본 이
- (중요) Command Line Interface에 거부감이 없는 이
- "나 개발자야~" 티 내보고 싶은 이(?)

## Why Git CLI?

- Git은 기본적으로 CLI 형태의 터미널을 사용하도록 고안
- Git의 모든 기능을 지원하는 것은 CLI 뿐 (공식문서)
- CLI는 별도의 툴이 필요하지 않다. 그저 terminal만 열면 될 뿐.
- GUI는 툴이 바뀌면 새로 사용법을 익혀야 하지만, CLI는 그럴 이유가 없다. terminal은 terminal이니까.
- 당연히(?) 그래픽을 사용하지 않으므로 GUI에 비해 빠르다.

### 이 학습에 적절하지 않은 분

- Git을 `commit`/`checkout`/`push`/`pull` 정도의 간단한 수준만이 필요한 이

  CLI보다는 GUI 툴을 이용하는 편이 정신건강에 이롭습니다.

- GitHub Blog를 써보려는 것만이 목적인 분

  마찬가지로 CLI보다는 GUI 툴을 이용하는 편이 정신건강에 이롭습니다. <br>
  이 스터디에서는 Static Site Generators에 대한 학습은 이루어지지 않습니다.


## 필요 사전 지식

본 학습을 위해서는 아래와 같은 사전 지식이 필요합니다.

- *(optional)* Linux(bash/shell) 기본 명령어

  Linux 기본 명령어를 몰라도 실습하는 것에는 무리가 없지만, 학습 자료에 모든 설명이 bash
  명령어로 되어 있으므로 bash 명령어에 익숙하지 않으면 이해가 어려울 수 있습니다.

  > 실제로 "디렉토리 생성"이나 "파일(html 등) 생성"에 대한 설명이 bash로 되어 있을 때,
  > Windows 환경에만 익숙한 분들(마우스 클릭으로만 폴더나 파일을 만들어 본 분들) 다수가
  > "디렉토리 생성", "파일 생성"을 하지 못한채 계속 생성을 어떻게 해야하는지 질문이
  > 들어오거나 스터디 이후에 해당 명령어를 어떻게 쓰라는 건지를 모르겠다는 질문이 더러
  > 들어옵니다.

  최소한으로 알고 있어야 하는 명령어는 다음과 같습니다.

  + 디렉토리 이동 : `cd`
    ```bash
    cd ..         # 상위 디렉토리 이동
    cd ./images   # 현재 디렉토리의 하위 images 디렉토리로 이동
    ```
  + 파일 목록 보기 : `ls`
    ```bash
    ls            # 현재 디렉토리의 파일 목록 보기
    ls -a         # 현재 디렉토리의 모든 파일 목록 보기 (숨김파일 포함)
    ```
  + 디렉토리 생성 : `mkdir`
    ```bash
    mkdir git-playground     #현재 디렉토리에 'git-example' 디렉토리 생성
    ```
  + 파일 삭제 : `rm`
    ```bash
    rm README.md          # README.md 파일 삭제
    rm ./images/ -r       # images 디렉토리 삭제
    ```
  + 빈 파일 생성 : `touch`
    ```bash
    touch README.md       # 0byte README.md 파일 생성
    ```

- *(optional)* vi(m) 에디터 사용 방법

  Git default editor로 vi를 기준으로 설명됩니다. vi외 다른 것을 사용하시는 분의 경우는
  별도 학습할 필요가 없으나 기존에 사용하시던 것이 없는 분이나 학습 자료와 동일한 환경으로
  연습하실 분은 vi 에디터에 대한 사용법을 알고 계셔야 합니다.

  스터디 중에 설명을 드리기는 하지만, 해당 사용법을 알고 계셔야 실습을 원활하게 진행하실 수
  있습니다.

  학습은 다음 동영상이나 사이트를 이용해보시면 됩니다.
  + [학습 동영상](https://www.youtube.com/embed/XvLQEUp3lLE)
  + [학습 블로그](https://macinjune.com/all-posts/mac/terminal/%EB%A7%A5-%ED%84%B0%EB%AF%B8%EB%84%90-vi-editor%EC%82%AC%EC%9A%A9%EB%B2%95-1%ED%8E%B8/)

  연습이 필요하신 경우,

  + Mac 사용자 분들은 terminal에서
  + Windows 사용자분들은
    - Git을 이미 설치한 분들은 Git Bash에서 또는,
    - 웹브라우저에서 [Unix Terminal Online](http://www.tutorialspoint.com/unix_terminal_online.php)로 접속하여

  연습해 보실 수 있습니다.

- English

  영어를 읽는데 거부감이 없으셔야 합니다. <br>
  Git은 모든 메세지 출력을 영어로 하고 있기 때문에 어쩔 수 없이 영어를 읽는걸 거부해서는
  아무 것도 할 수 없습니다. (적어도 성공했다는건지 오류가 났다는건지는 파악을 해야...)

  종종 영어로 나오는데 무언가 오류가 나서 원하는 결과가 나오지 않을 때, 영어 + 오류에 대한
  거부 반응으로 아예 읽지도 않고 '저거 뭐야... 무서워...'만 시전되는 경우가 많습니다...

  컴퓨터는 그렇게 쉽게 고장나지 않으니 걱정 마시고 그냥 뭐가 안되는건지 읽고 앞으로 뭘 해야
  하는지를 이해하면 됩니다. Git은 제법 친절하게 알려줍니다. 다만 한국어를 할 줄 몰라서 그렇지...

## 준비물

본 학습을 위해서는 아래와 같은 준비물이 필요합니다.

- *(required)* 개인 노트북
- *(optional)* 장시간 학습을 대비한 체력
- *(optional)* 떨어지는 당을 보충할 소소한 개인 간식거리 (흘리지만 마세요....)

## 스터디 내용

> 스터디 자료가 기존 것에서 약간 편집되는 중이라 아래 내용의 순서가 변경될 수 있습니다.

- 도입
  + Git이란?
    - 버전 관리 시스템이란?
  + 왜 Git을 사용하나?
    - 나 혼자 쓴다
    - 협업하는 경우

- Git 설치
  + 다운로드
    - Mac OS X
    - Windows
  + Git 설정
    - 사용자 설정
    - 사용자 설정 확인

- Git 기초편
  + 저장소 만들기
    - 관리하지 않을 파일 설정하기
  + 저장소에 변경점 기록하기
    - git의 3가지 상태
      * git의 파일 관리 흐름
      * Working Directory
      * Staging Area
      * Local Repository
      * File LifeCycle
    - 상태 확인하기
    - commit 할 준비 하기
    - commit 하기
  + commit 기록 확인하기

- Git 발전편
  + Branch
    - branch 생성 & 확인
    - branch 이동하기
    - 특정 commit으로부터 branch 생성하기
      * 특정 commit으로 이동하기
    - 새로운 branch에서 작업하기
    - 변경점 병합하기
      * 충돌 다루기
        * 병합 취소
        * 병합 충돌 해결하기
    - branch rebae하기
    - branch 지우기
  + Stash
    - stash 상태 확인하기
    - 이름을 지정하여 임시로 변경 저장하기
    - stash 적용하기
    - stash 항목 삭제하기
  + 변경 취소하기
    - staged 파일 취소
    - 파일 수정 내역 폐기
    - 특정 commit 원복시키기
  + 기록 재작성
    - 마지막 commit 변경하기
    - commit 되돌리기
      * 마지막 commit 되돌리기
      * 특정 coomit 으로 되돌리기
      * n-번째 이전 commit으로 되돌리기
    - Rebasing Commits
      * 여러 commit들 메세지 변경하기
      * 이전 commit들 수정하기
      * commit 순서 조정하기
      * commit 합치기
      * commit 삭제하기

- 원격 저장소
  + Git 호스팅 서비스
  + 원격 저장소에 연결하기
    - Github에 새 저장소 만들기
    - 로컬 branch 게시하기
    - 로컬 branch와 원격 branch 확인하기
    - 원격의 변경 통합시키기
    - 원격 branch 삭제하기
  + 원격으로부터 저장소 복제하기
  + GitHub 프로젝트에 기여하기

- 남은 시간 워크샵
---
1. <a id="foot-cli" href="#cli">Command Line Interface</a>

  명령 줄 인터페이스 (또는 명령어 인터페이스).  텍스트 터미널을 통해 작업을 진행하는 방법.

  windows의 경우는 명령 프롬프트, Mac, Linux등의 경우는 terminal이 이에 해당.

2. <a id="foot-gui" href="#gui">Graphic User Interface Tool</a>

  마우스로 클릭, 드래그앤드롭으로 사용할 수있는 툴 <br>
  SourceTree, GitHub Desktop, GitKraken 등등