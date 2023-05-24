---
title: 값 암호화
description: Reactor API를 사용할 때 중요한 값을 암호화하는 방법에 대해 알아봅니다.
exl-id: d89e7f43-3bdb-40a5-a302-bad6fd1f4596
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 1%

---

# 값 암호화

Adobe Experience Platform에서 태그를 사용하는 경우 일부 워크플로에서는 민감한 값을 제공해야 합니다(예: 호스트를 통해 환경에 라이브러리를 전달할 때 개인 키를 제공). 이러한 자격 증명의 민감한 특성으로 인해 안전한 전송 및 저장이 필요합니다.

이 문서에서는 다음을 사용하여 중요한 값을 암호화하는 방법에 대해 설명합니다. [GnuPG 암호화](https://www.gnupg.org/gph/en/manual/x110.html) (GPG라고도 함) 태그 시스템만 읽을 수 있습니다.

## 공개 GPG 키 및 체크섬 가져오기

다음 이후 [다운로드 중](https://gnupg.org/download/) 최신 버전의 GPG를 설치하려면 태그 프로덕션 환경에 대한 공개 GPG 키를 받아야 합니다.

* [GPG 키](https://github.com/adobe/reactor-developer-docs/blob/master/files/launch%40adobe.com_pub.gpg)
* [체크섬](https://github.com/adobe/reactor-developer-docs/blob/master/files/launch%40adobe.com_pub.gpg.sum)

## 키를 키 체인으로 가져오기

키를 컴퓨터에 저장했으면 다음 단계로 GPG 키체인에 키를 추가합니다.

**구문**

```shell
gpg --import {KEY_NAME}
```

| 매개변수 | 설명 |
| --- | --- |
| `{KEY_NAME}` | 공개 키 파일의 이름입니다. |

{style="table-layout:auto"}

**예**

```shell
gpg --import launch@adobe.com_pub.gpg
```

## 값 암호화

키체인에 키를 추가한 후 `--encrypt` 플래그. 다음 스크립트는 이 명령의 작동 방식을 보여 줍니다.

```shell
echo -n 'Example value' | gpg --armor --encrypt -r "Tags Data Encryption <launch@adobe.com>"
```

이 명령은 다음과 같이 분류할 수 있습니다.

* 입력이 `gpg` 명령입니다.
* `--armor` 는 이진수 대신 ASCII 지원 출력을 생성합니다. 따라서 JSON을 통해 값을 전송하는 작업이 간소화됩니다.
* `--encrypt` gpg에 데이터를 암호화하도록 지시합니다.
* `-r` 데이터의 수신자를 설정합니다. 수신자(공개 키에 해당하는 개인 키의 소유자)만이 데이터를 해독할 수 있다. 원하는 키의 수신자 이름은 의 출력을 검사하여 찾을 수 있습니다. `gpg --list-keys`.

위의 명령은 다음에 대해 공개 키를 사용합니다. `Tags Data Encryption <launch@adobe.com>` 값을 암호화하려면 `Example value`, ASCII-Armed 형식

명령 출력은 다음과 비슷합니다.

```shell
-----BEGIN PGP MESSAGE-----

hQIMAxJHCI6fydT/ARAAwQ0Y0k7eSAbd0T9seoaWX75G70O2gxAF20KY5FWiZ9/m
/RkgJwhJusZyEdazC/CmAdfXi9bsVxQT0i06ErUxXfQF0VtweRlcyRBsxzLz6Hr+
BpYGnq+cCCzGAT73Gg1CM4UWmaPKLLyWKGkXtDBAqVBRAIQT/8JhnkbyWIohHkWV
I/Uf7NrPXuaSmrqZ1SZQgwjIM3qNMR02qtqg59dncKoCQBji8Oeb8lqRLskRT0Jq
gVgbJYwSe2n6KpJkELJ6QtF9lCRl1+yU4mvM4jBHgkM1+vb1WmbFRIR40dDpg85N
0J9hVj4bg//eLRDfAdEC9kgq9Atph0WqJ5EpehdS7yVO9lO8mpbpqZ4BCGjTi/VS
isEPr6eZ2mxRbk8f9Z4csRZnkErY8ep5+cqC5CZVdmguWvC9PKzXqEsPFd0PSYk3
Qp3UIW2/JMf16E5CKmntm+gKdl6kggZOOvNQuyJYa9yNbzySPerHXsknTOxV+QP/
WXwrAL52g5+gpMib7Ve/KBz5/OViDhDqkmHzlGad73W74d+CYjf0AnuXuWRRlUMT
s8ORw1eplInldhXk2mgkGPZS/gWDs3zpKUu4GSO9AaeWldynLG/Bgh78XhumQ58h
ekGD+p3PyyvxjfS5G/wf9HQZ085+mnjpKFa7fuFBQPbg4WpBadhWrhobthC+hN3S
SAE9yWU11Y3xpoxqg4y7iYZ6rnX+qP2oUNYxC2/hdhsFbbZtUh4s51qaoLbe0iWB
OUoIPf4KxTaboHZOEy32ZBng5heVrn4i9w==
=jrfE
-----END PGP MESSAGE-----
```

이 출력은 다음에 해당하는 개인 키가 있는 시스템에서만 해독할 수 있습니다. `Tags Data Encryption <launch@adobe.com>` 공개 키.

이 출력은 Reactor API로 데이터를 전송할 때에서 제공해야 하는 값입니다. 시스템은 이 암호화된 출력을 저장하고 필요에 따라 일시적으로 해독한다. 예를 들어, 시스템은 서버 연결을 시작할 수 있을 만큼 충분한 시간 동안 호스트 자격 증명을 해독한 다음 해독된 값의 모든 추적을 즉시 제거합니다.

>[!NOTE]
>
>장갑되고 암호화된 값의 형식이 중요합니다. 라인 반환이 요청에 제공된 값에서 제대로 이스케이프되는지 확인합니다.
