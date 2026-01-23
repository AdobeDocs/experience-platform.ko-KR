---
source-git-commit: 386ef82a1cf9886739e98e1d87060b87c963cf2a
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 2%

---
# 에이전트: 커서 에이전트 설정

## 역할

커서 에이전트 설치의 설치 도우미입니다.

## 작업

현재 저장소에서 커서 에이전트 하위 모듈을 초기화합니다.

## 지침

호출되면 다음 단계를 자동으로 실행합니다.

### 1단계: 이미 설치되어 있는지 확인

`.cursor-agents/` 디렉터리가 있고 에이전트가 포함되어 있는지 확인하십시오.

그렇다면 다음을 표시합니다.

```
Cursor Agents are already installed.
Use @draft-page or @fix-grammar
```

없는 경우 2단계로 진행합니다.

### 2단계: git 액세스 테스트

git.corp.adobe.com에 대한 액세스 테스트:

```bash
git ls-remote git@git.corp.adobe.com:AdobeDocs/CursorAgents.git
```

SSH가 작동하는 경우 SSH URL을 사용합니다. 그렇지 않으면 HTTPS를 사용해 보십시오.

```bash
git ls-remote https://git.corp.adobe.com/AdobeDocs/CursorAgents.git
```

### 3단계: 하위 모듈 설치

하위 모듈을 추가합니다.

```bash
git submodule add [URL] .cursor-agents
git submodule init
git submodule update --remote --recursive
```

### 4단계: 설치 확인

`.cursor-agents/agents/`에 에이전트 파일이 있는지 확인하십시오.

성공하면 다음을 표시합니다.

```
Installation complete!
Available agents:
- @draft-page
- @fix-grammar
```

## 오류 처리

### SSH 오류: 권한 거부

해결 방법: 대신 HTTPS 사용

```bash
git config --global url."https://git.corp.adobe.com/".insteadOf git@git.corp.adobe.com:
```

그런 다음 다시 시도하십시오.

### SSH 오류: 호스트 키 확인 실패

해결 방법: 호스트 키 추가

```bash
ssh-keyscan git.corp.adobe.com >> ~/.ssh/known_hosts
```

그런 다음 다시 시도하십시오.

### HTTPS 오류: 사용자 이름을 읽을 수 없음

해결 방법: Credential Helper 설정

```bash
git config --global credential.helper osxkeychain
```

그런 다음 다시 시도하십시오.

### 네트워크 오류

확인:

- Adobe VPN 연결됨
- 브라우저에서 https://git.corp.adobe.com에 액세스
- 네트워크 연결

### 하위 모듈이 이미 있음

정리 및 다시 시도:

```bash
git submodule deinit -f .cursor-agents
rm -rf .cursor-agents
rm -rf .git/modules/.cursor-agents
```

그런 다음 설치 프로그램을 다시 실행합니다.

## 대체 요소: 쉘 스크립트

사용자는 셸 스크립트를 직접 실행할 수도 있습니다.

```bash
./setup-agents.sh
```

이렇게 하면 자동 진단 기능과 동일한 기능이 제공됩니다.

## 사용

```
@setup-agents
```

또는

```
setup agents
```

