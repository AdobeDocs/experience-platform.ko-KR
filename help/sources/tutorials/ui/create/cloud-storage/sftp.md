---
keywords: Experience Platform;홈;인기 항목;SFTP;sftp
solution: Experience Platform
title: UI에서 SFTP 소스 연결 만들기
topic-legacy: overview
type: Tutorial
description: Adobe Experience Platform UI를 사용하여 SFTP 소스 연결을 만드는 방법을 알아봅니다.
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: ade0da445b18108a7f8720404cc7a65139ed42b1
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 0%

---

# UI에서 [!DNL SFTP] 소스 연결 만들기

이 자습서에서는 Adobe Experience Platform UI를 사용하여 [!DNL SFTP] 소스 연결을 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 작성 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 빌딩 블록에 대해 알아봅니다.
   * [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아보십시오.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

>[!IMPORTANT]
>
>[!DNL SFTP] 소스 연결을 사용하여 JSON 개체를 섭취할 때 줄바꿈 또는 캐리지 리턴 발생을 방지하는 것이 좋습니다. 제한 사항을 해결하려면 행당 단일 JSON 개체를 사용하고 후속 파일에 여러 줄을 사용합니다.

이미 유효한 [!DNL SFTP] 연결이 있는 경우 이 문서의 나머지 부분을 건너뛰고 [데이터 흐름](../../dataflow/batch/cloud-storage.md) 구성에서 자습서를 진행할 수 있습니다.

### 필요한 자격 증명 수집

[!DNL SFTP]에 연결하려면 다음 연결 속성에 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `host` | [!DNL SFTP] 서버와 연결된 이름 또는 IP 주소입니다. |
| `port` | 연결할 [!DNL SFTP] 서버 포트입니다. 지정하지 않으면 기본값은 `22`입니다. |
| `username` | [!DNL SFTP] 서버에 액세스할 수 있는 사용자 이름입니다. |
| `password` | [!DNL SFTP] 서버의 암호입니다. |
| `privateKeyContent` | Base64로 인코딩된 SSH 개인 키 콘텐츠입니다. OpenSSH 키 유형은 RSA 또는 DSA로 분류해야 합니다. |
| `passPhrase` | 키 파일 또는 키 컨텐츠가 암호 구문으로 보호되는 경우 개인 키를 해독하기 위한 암호 구문 또는 암호입니다. PrivateKeyContent가 암호로 보호된 경우 이 매개 변수는 PrivateKeyContent의 암호와 함께 값으로 사용해야 합니다. |

필요한 자격 증명을 수집하면 아래 단계에 따라 Platform에 연결할 새 [!DNL SFTP] 계정을 만들 수 있습니다.

## [!DNL SFTP] 서버에 연결

플랫폼 UI의 왼쪽 탐색 막대에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 공간에 액세스합니다. [!UICONTROL 카탈로그] 화면에는 로 인바운드 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

[!UICONTROL 클라우드 저장소] 카테고리에서 **[!UICONTROL SFTP]** 를 선택한 다음 **[!UICONTROL 데이터 추가]**&#x200B;를 선택합니다.

![카탈로그](../../../../images/tutorials/create/sftp/catalog.png)

**[!UICONTROL SFTP에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 연결하려면 연결할 FTP 또는 SFTP 계정을 선택한 다음 **[!UICONTROL 다음]**&#x200B;을 선택하여 계속 진행합니다.

![기존](../../../../images/tutorials/create/sftp/existing.png)

### 새 계정

새 계정을 만드는 경우 **[!UICONTROL 새 계정]**&#x200B;을 선택한 다음 새 [!DNL SFTP] 계정에 대한 이름과 설명을 입력합니다.

#### 암호를 사용하여 인증

[!DNL SFTP] 은 액세스를 위해 다른 인증 유형을 지원합니다. **[!UICONTROL 계정 인증]**&#x200B;에서 **[!UICONTROL 암호]**&#x200B;를 선택한 다음 사용자 이름과 암호와 함께 연결할 호스트 및 포트 값을 제공합니다.

![connect-password](../../../../images/tutorials/create/sftp/password.png)

#### SSH 공개 키를 사용하여 인증

SSH 공개 키 기반 자격 증명을 사용하려면 **[!UICONTROL SSH 공개 키]**&#x200B;를 선택한 다음 호스트 및 포트 값과 개인 키 컨텐츠 및 암호 조합을 제공합니다.

>[!IMPORTANT]
>
>SFTP는 RSA 또는 DSA 유형인 OpenSSH 키를 지원합니다. 키 파일 컨텐츠가 `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"`으로 시작하고 `"-----END [RSA/DSA] PRIVATE KEY-----"`로 끝나야 합니다. 개인 키 파일이 PPK 형식 파일인 경우 PuTTY 도구를 사용하여 PPK에서 OpenSSH 형식으로 변환합니다.

![connect-ssh](../../../../images/tutorials/create/sftp/ssh-public-key.png)

| 자격 증명 | 설명 |
| ---------- | ----------- |
| 개인 키 콘텐츠 | Base64로 인코딩된 SSH 개인 키 콘텐츠입니다. OpenSSH 키 유형은 RSA 또는 DSA로 분류해야 합니다. |
| 암호 | 키 파일 또는 키 컨텐츠가 암호 구문으로 보호되는 경우 개인 키를 해독할 암호 구문 또는 암호를 지정합니다. PrivateKeyContent가 암호로 보호된 경우 이 매개 변수는 PrivateKeyContent의 암호와 함께 해당 값으로 사용해야 합니다. |


## 다음 단계

이 자습서를 따라 SFTP 계정에 대한 연결을 설정했습니다. 이제 다음 자습서를 계속 진행하고 [데이터 흐름을 구성하여 클라우드 저장소에서 Platform](../../dataflow/batch/cloud-storage.md)로 데이터를 가져올 수 있습니다.
