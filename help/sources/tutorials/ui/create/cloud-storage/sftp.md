---
keywords: Experience Platform;홈;인기 항목;SFTP;sftp
solution: Experience Platform
title: UI에서 SFTP 소스 연결 만들기
topic: overview
type: Tutorial
description: Adobe Experience Platform UI를 사용하여 SFTP 소스 연결을 만드는 방법을 알아봅니다.
translation-type: tm+mt
source-git-commit: 0e11acc4a599d360cb3048445003f61848ad23d3
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 1%

---


# UI에서 SFTP 소스 연결 만들기

이 자습서에서는 Adobe Experience Platform UI를 사용하여 SFTP 소스 연결을 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md):Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md):스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 블록에 대해 알아봅니다.
   * [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md):스키마 편집기 UI를 사용하여 사용자 정의 스키마를 생성하는 방법을 알아봅니다.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

>[!IMPORTANT]
>
>SFTP 소스 연결을 사용하여 JSON 개체를 인제스트할 때 뉴라인 또는 캐리지 리턴이 발생하지 않는 것이 좋습니다. 제한 사항을 해결하려면 라인당 단일 JSON 개체를 사용하고 이후 파일에 대해 여러 행을 사용하십시오.

유효한 SFTP 연결이 이미 있는 경우 이 문서의 나머지 부분을 건너뛰고 [데이터 흐름 구성](../../dataflow/batch/cloud-storage.md)에서 자습서로 진행할 수 있습니다.

### 필요한 자격 증명 수집

SFTP에 연결하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `host` | SFTP 서버와 연결된 이름 또는 IP 주소입니다. |
| `username` | SFTP 서버에 액세스할 수 있는 사용자 이름입니다. |
| `password` | SFTP 서버의 암호입니다. |
| `privateKeyContent` | Base64 인코딩된 SSH 개인 키 콘텐츠입니다. OpenSSH 키 유형은 RSA 또는 DSA로 분류되어야 합니다. |
| `passPhrase` | 키 파일 또는 키 내용이 암호 구문으로 보호되는 경우 개인 키를 해독하기 위한 암호 구문 또는 암호입니다. PrivateKeyContent가 암호로 보호되는 경우 이 매개 변수를 PrivateKeyContent 암호와 함께 값으로 사용해야 합니다. |

필요한 자격 증명을 수집했으면 아래 절차에 따라 플랫폼에 연결할 새 SFTP 계정을 만들 수 있습니다.

## SFTP 서버에 연결

[Adobe Experience Platform](https://platform.adobe.com)에 로그인한 다음 왼쪽 탐색 막대에서 **[!UICONTROL Sources]**&#x200B;를 선택하여 [!UICONTROL Sources] 작업 영역에 액세스합니다. [!UICONTROL Catalog] 화면에는 인바운드 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면의 왼쪽에 있는 카탈로그에서 적절한 범주를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

[!UICONTROL Cloud storage] 범주에서 **[!UICONTROL SFTP]**&#x200B;을 선택합니다. 이 커넥터를 처음 사용하는 경우 **[!UICONTROL Configure]** 을 선택합니다. 그렇지 않은 경우 **[!UICONTROL Add data]**&#x200B;을 선택하여 새 SFTP 연결을 만듭니다.

![카탈로그](../../../../images/tutorials/create/sftp/catalog.png)

**[!UICONTROL Connect to SFTP]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명이나 기존 자격 증명을 사용할 수 있습니다.

### 새 계정

새 자격 증명을 사용 중인 경우 **[!UICONTROL New account]**&#x200B;을 선택합니다. 표시되는 입력 양식에서 이름, 선택적 설명 및 자격 증명을 제공합니다. 완료되면 **[!UICONTROL Connect]**&#x200B;을 선택한 다음 새 연결이 설정될 때까지 잠시 기다려 주십시오.

SFTP 커넥터는 액세스할 수 있는 서로 다른 인증 유형을 제공합니다. 암호 기반 자격 증명을 사용하려면 **[!UICONTROL Account authentication]** 아래에서 **[!UICONTROL Password]**&#x200B;을 선택합니다.

![connect-password](../../../../images/tutorials/create/sftp/password.png)

또는 **[SSH 공개 키]**&#x200B;를 선택하고 [!UICONTROL Private key content] 및 [!UICONTROL Passphrase]의 조합을 사용하여 SFTP 계정을 연결할 수 있습니다.

>[!IMPORTANT]
>
>SFTP 커넥터는 RSA 또는 DSA 유형 OpenSSH 키를 지원합니다. 키 파일 내용이 `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"`으로 시작하고 `"-----END [RSA/DSA] PRIVATE KEY-----"`로 끝나야 합니다. 개인 키 파일이 PPK 형식 파일인 경우 PuTTY 도구를 사용하여 PPK에서 OpenSSH 형식으로 변환합니다.

![connect-ssh](../../../../images/tutorials/create/sftp/ssh.png)

| 자격 증명 | 설명 |
| ---------- | ----------- |
| 개인 키 컨텐츠 | Base64 인코딩된 SSH 개인 키 콘텐츠입니다. OpenSSH 키 유형은 RSA 또는 DSA로 분류되어야 합니다. |
| 암호 | 키 파일 또는 키 콘텐트가 암호 구문으로 보호되는 경우 개인 키를 해독할 암호 구문 또는 암호를 지정합니다. PrivateKeyContent가 암호로 보호되는 경우 이 매개 변수를 PrivateKeyContent 암호와 함께 값으로 사용해야 합니다. |

### 기존 계정

기존 계정을 연결하려면 연결할 FTP 또는 SFTP 계정을 선택한 다음 **[!UICONTROL Next]**&#x200B;을 선택하여 계속 진행합니다.

![기존](../../../../images/tutorials/create/sftp/existing.png)

## 다음 단계

이 자습서를 따라 FTP 또는 SFTP 계정에 대한 연결을 설정했습니다. 이제 다음 튜토리얼을 계속 진행할 수 있으며 [데이터 흐름 구성을 통해 클라우드 스토리지의 데이터를 플랫폼](../../dataflow/batch/cloud-storage.md)으로 가져올 수 있습니다.