---
title: 값 암호화
description: Reactor API를 사용할 때 중요한 값을 암호화하는 방법을 알아봅니다.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 1%

---

# 값 암호화

Adobe Experience Platform에서 태그를 사용할 때 일부 워크플로우에서는 중요한 값을 제공해야 합니다(예: 호스트를 통해 라이브러리를 환경에 제공할 때 개인 키 제공). 이러한 자격 증명의 중요한 특성은 다음과 같습니다
보안 전송 및 스토리지

이 문서에서는 태그 시스템만 읽을 수 있도록 [GnuPG 암호화](https://www.gnupg.org/gph/en/manual/x110.html)(GPG라고도 함)를 사용하여 중요한 값을 암호화하는 방법에 대해 설명합니다.

## 공개 GPG 키 및 체크섬 가져오기

[다운로드](https://gnupg.org/download/) 및 최신 버전의 GPG를 설치한 후 태그 프로덕션 환경에 대한 공개 GPG 키를 받아야 합니다.

* [GPG 키](https://github.com/adobe/reactor-developer-docs/blob/master/files/launch%40adobe.com_pub.gpg)
* [체크섬](https://github.com/adobe/reactor-developer-docs/blob/master/files/launch%40adobe.com_pub.gpg.sum)

## 키체인으로 키 가져오기

키를 컴퓨터에 저장하면 다음 단계는 GPG 키 체인에 추가하는 것입니다.

**구문**

```shell
gpg --import {KEY_NAME}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{KEY_NAME}` | 공개 키 파일의 이름입니다. |

{style=&quot;table-layout:auto&quot;}

**예**

```shell
gpg --import launch@adobe.com_pub.gpg
```

## 값 암호화

키 체인에 키를 추가한 후 `--encrypt` 플래그를 사용하여 값 암호화를 시작할 수 있습니다. 다음 스크립트는 이 명령이 작동하는 방식을 보여 줍니다.

```shell
echo -n 'Example value' | gpg --armor --encrypt -r "Tags Data Encryption <launch@adobe.com>"
```

이 명령은 다음과 같이 분류할 수 있습니다.

* `gpg` 명령에 입력이 제공됩니다.
* `--armor` 이진 대신 ASCII 기갑 출력을 만듭니다. 이렇게 하면 JSON을 통해 값을 전송하는 작업이 간소화됩니다.
* `--encrypt` 는 GPG에 데이터를 암호화하도록 지시합니다.
* `-r` 데이터에 대한 수신자를 설정합니다. 받는 사람(공개 키에 해당하는 개인 키의 소유자)만 데이터를 해독할 수 있습니다. 원하는 키의 수신자 이름은 `gpg --list-keys` 출력을 검사하여 찾을 수 있습니다.

위의 명령에서는 `Tags Data Encryption <launch@adobe.com>`에 대한 공개 키를 사용하여 `Example value` 값을 ASCII 형식의 암호화합니다.

명령의 출력은 다음과 비슷합니다.

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

이 출력은 개인 키가 있는 시스템에서만 암호화할 수 있습니다.
는 `Tags Data Encryption <launch@adobe.com>` 공개 키에 해당합니다.

이 출력은 Reactor API로 데이터를 전송할 때 제공해야 하는 값입니다. 시스템은 이 암호화된 출력을 저장하고 필요에 따라 일시적으로 해독합니다. 예를 들어, 시스템은 서버에 대한 연결을 시작할 수 있을 만큼 오랫동안 호스트 자격 증명을 해독한 다음 즉시 해독된 값의 모든 추적을 제거합니다.

>[!NOTE]
>
>장갑의 암호화된 값의 포맷은 중요합니다. 요청에 제공된 값에서 라인 반품이 제대로 이스케이프되는지 확인합니다.
