---
keywords: Experience Platform;home;popular topics;SFTP;sftp
solution: Experience Platform
title: UI에서 SFTP 소스 커넥터 만들기
topic: overview
type: Tutorial
description: 이 자습서에서는 플랫폼 사용자 인터페이스를 사용하여 SFTP 소스 커넥터를 만드는 단계를 제공합니다.
translation-type: tm+mt
source-git-commit: 7b638f0516804e6a2dbae3982d6284a958230f42
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---


# UI에서 SFTP 소스 커넥터 만들기

>[!NOTE]
>
>SFTP 커넥터가 베타에 있습니다. 베타 [레이블이 지정된 커넥터 사용에 대한 자세한 내용은 소스 개요를](../../../../home.md#terms-and-conditions) 참조하십시오.

이 자습서에서는 플랫폼 사용자 인터페이스를 사용하여 SFTP 소스 커넥터를 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 다음 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md):Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md):스키마 컴포지션의 주요 원칙 및 모범 사례 등 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md):스키마 편집기 UI를 사용하여 사용자 정의 스키마를 생성하는 방법을 알아봅니다.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 유효한 SFTP 연결이 있는 경우 이 문서의 나머지 부분을 건너뛰고 데이터 흐름 [구성에 대한 자습서로 진행할 수 있습니다](../../dataflow/batch/cloud-storage.md).

### 필요한 자격 증명 수집

SFTP에 연결하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `host` | SFTP 서버와 연결된 이름 또는 IP 주소입니다. |
| `username` | SFTP 서버에 액세스할 수 있는 사용자 이름입니다. |
| `password` | SFTP 서버의 암호입니다. |
| `privateKeyContent` | Base64로 인코딩된 SSH 개인 키 콘텐츠입니다. SSH 개인 키 OpenSSH(RSA/DSA) 형식입니다. |
| `passPhrase` | 키 파일 또는 키 콘텐트가 암호 구문으로 보호되는 경우 개인 키를 해독하기 위한 암호 구문 또는 암호입니다. PrivateKeyContent가 암호로 보호된 경우 이 매개 변수를 PrivateKeyContent 암호와 함께 값으로 사용해야 합니다. |

필요한 자격 증명을 수집했으면 아래 절차에 따라 플랫폼에 연결할 새 SFTP 계정을 만들 수 있습니다.

## SFTP 서버에 연결

[Adobe Experience Platform](https://platform.adobe.com) 에 로그인한 다음 **** 왼쪽 탐색 막대에서 소스를 선택하여 [!UICONTROL 소스 작업 영역에] 액세스합니다. [ [!UICONTROL 카탈로그] ] 화면에는 인바운드 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면의 왼쪽에 있는 카탈로그에서 해당 범주를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

클라우드 [!UICONTROL 스토리지] 카테고리 아래에서 **[!UICONTROL SFTP를 선택합니다]**. 이 커넥터를 처음 사용하는 경우 구성을 **[!UICONTROL 선택합니다]**. 그렇지 않은 경우 데이터 **[!UICONTROL 추가를]** 선택하여 새 SFTP 연결을 만듭니다.

![카탈로그](../../../../images/tutorials/create/sftp/catalog.png)

SFTP에 **[!UICONTROL 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명이나 기존 자격 증명을 사용할 수 있습니다.

### 새 계정

새 자격 증명을 사용 중인 경우 **[!UICONTROL 새 계정을 선택합니다]**. 표시되는 입력 양식에서 이름, 선택적 설명 및 자격 증명을 제공합니다. 완료되면 **[!UICONTROL Connect를]** 선택한 다음 새 연결이 설정될 때까지 잠시 기다립니다.

SFTP 커넥터는 액세스할 수 있는 서로 다른 인증 유형을 제공합니다. 계정 **[!UICONTROL 인증]** 아래에서 **[!UICONTROL 암호]** 기반 자격 증명을 사용하려면 암호를 선택합니다.

![connect-password](../../../../images/tutorials/create/sftp/password.png)

또는 **[SSH 공개 키를]** 선택하고 [!UICONTROL 개인 키 컨텐츠] 및 암호를 조합하여 SFTP 계정을 연결할 수 [!UICONTROL 있습니다].

>[!IMPORTANT]
>
>SFTP 커넥터는 RSA/DSA OpenSSH 키를 지원합니다. 키 파일 컨텐츠가 다음으로 시작되는지 확인합니다 `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"`. 개인 키 파일이 PPK 형식 파일인 경우 PuTTY 도구를 사용하여 PPK에서 OpenSSH 형식으로 변환합니다.

![connect-ssh](../../../../images/tutorials/create/sftp/ssh.png)

| 자격 증명 | 설명 |
| ---------- | ----------- |
| 개인 키 컨텐츠 | Base64로 인코딩된 SSH 개인 키 컨텐츠입니다. SSH 개인 키는 OpenSSH 형식이어야 합니다. |
| 암호 | 키 파일 또는 키 콘텐트가 암호 구문으로 보호되는 경우 개인 키를 해독하기 위한 비밀번호 구문 또는 암호를 지정합니다. PrivateKeyContent가 암호로 보호된 경우 이 매개 변수를 PrivateKeyContent 암호와 함께 값으로 사용해야 합니다. |

### 기존 계정

기존 계정을 연결하려면 연결할 FTP 또는 SFTP 계정을 선택한 다음 **[!UICONTROL 다음을]** 선택하여 진행하십시오.

![기존](../../../../images/tutorials/create/sftp/existing.png)

## 다음 단계

이 자습서를 따라 FTP 또는 SFTP 계정에 대한 연결을 설정했습니다. 이제 다음 튜토리얼로 계속 진행하여 데이터 흐름을 [구성하여 클라우드 스토리지의 데이터를 Platform으로 가져올 수 있습니다](../../dataflow/batch/cloud-storage.md).