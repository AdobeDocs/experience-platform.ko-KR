---
title: UI에서 SFTP Source 연결 만들기
description: Adobe Experience Platform UI를 사용하여 SFTP 소스 연결을 만드는 방법을 알아봅니다.
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: 4816a6b627dc6551e351bfe3cdc4bc8c8ea8b17e
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 1%

---

# UI에서 [!DNL SFTP] 소스 연결 만들기

이 자습서에서는 Adobe Experience Platform UI를 사용하여 [!DNL SFTP] 소스 연결을 만드는 단계를 제공합니다.

## 시작

이 자습서에서는 Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): Experience Platform에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

>[!IMPORTANT]
>
>[!DNL SFTP] 소스 연결을 사용하여 JSON 개체를 수집할 때 줄바꿈 또는 캐리지 리턴을 피하는 것이 좋습니다. 제한을 해결하려면 라인당 단일 JSON 개체를 사용하고 후속 파일에 여러 라인을 사용합니다.

이미 올바른 [!DNL SFTP] 연결이 있는 경우 이 문서의 나머지 부분을 건너뛰고 [데이터 흐름 구성](../../dataflow/batch/cloud-storage.md)에 대한 자습서로 진행할 수 있습니다.

### 필요한 자격 증명 수집

인증 자격 증명을 검색하는 방법에 대한 자세한 단계는 [[!DNL SFTP] 인증 안내서](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials)를 참조하십시오.

## [!DNL SFTP] 서버에 연결

Experience Platform UI의 왼쪽 탐색 모음에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 영역에 액세스합니다. [!UICONTROL 카탈로그] 화면에 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

[!UICONTROL 클라우드 저장소] 범주에서 **[!UICONTROL SFTP]**&#x200B;을(를) 선택한 다음 **[!UICONTROL 데이터 추가]**&#x200B;를 선택합니다.

![SFTP 원본이 있는 Experience Platform 원본 카탈로그를 선택했습니다.](../../../../images/tutorials/create/sftp/catalog.png)

**[!UICONTROL SFTP에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정에 연결하려면 연결할 FTP 또는 SFTP 계정을 선택한 다음 **[!UICONTROL 다음]**&#x200B;을 선택하여 계속합니다.

![Experience Platform UI에 있는 기존 SFTP 계정 목록입니다.](../../../../images/tutorials/create/sftp/existing.png)

### 새 계정

>[!TIP]
>
>* 만든 후에는 [!DNL SFTP] 기본 연결의 인증 유형을 변경할 수 없습니다. 인증 유형을 변경하려면 새 기본 연결을 만들어야 합니다.
>
>* SFTP는 `ed25519`, `RSA` 또는 `DSA` 형식의 OpenSSH 키를 지원합니다. 키 파일 내용이 `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"`(으)로 시작되고 `"-----END [RSA/DSA] PRIVATE KEY-----"`(으)로 끝나는지 확인하십시오. 개인 키 파일이 PPK 형식 파일인 경우 PuTTY 도구를 사용하여 PPK에서 OpenSSH 형식으로 변환합니다.

새 계정을 만드는 경우 **[!UICONTROL 새 계정]**&#x200B;을(를) 선택한 다음 새 [!DNL SFTP] 계정에 대한 이름과 선택적 설명을 입력하십시오.

![SFTP의 새 계정 화면](../../../../images/tutorials/create/sftp/new.png)

[!DNL SFTP] 원본은 기본 인증과 SSH 공개 키를 통한 인증을 모두 지원합니다.

>[!BEGINTABS]

>[!TAB 기본 인증]

기본 인증을 사용하려면 **[!UICONTROL 암호]**&#x200B;를 선택한 후 다음 자격 증명에 적절한 값을 입력하십시오.

* 호스트
* 포트
* 사용자 이름
* 암호

이 단계에서는 최대 동시 연결을 구성하고, 폴더 경로를 정의하고, [!DNL SFTP] 서버에 대한 청크를 활성화하거나 비활성화할 수도 있습니다. 완료되면 **[!UICONTROL 소스에 연결]**&#x200B;을 선택하고 연결을 설정할 수 있도록 잠시 기다립니다.

인증에 대한 자세한 내용은 [필요한 자격 증명 수집 [!DNL SFTP]](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials)에 대한 안내서를 참조하십시오.

![기본 인증을 사용하는 SFTP 원본에 대한 새 계정 화면](../../../../images/tutorials/create/sftp/password.png)

>[!TAB SSH 공개 키 인증]

SSH 공개 키 기반 자격 증명을 사용하려면 **[!UICONTROL SSH 공개 키]**&#x200B;를 선택한 후 다음 자격 증명에 적절한 값을 입력하십시오.

* 호스트
* 포트
* 사용자 이름
* 비공개 키 콘텐츠
* 암호구

이 단계에서는 최대 동시 연결을 구성하고, 폴더 경로를 정의하고, [!DNL SFTP] 서버에 대한 청크를 활성화하거나 비활성화할 수도 있습니다. 완료되면 **[!UICONTROL 소스에 연결]**&#x200B;을 선택하고 연결을 설정할 수 있도록 잠시 기다립니다.

인증에 대한 자세한 내용은 [필요한 자격 증명 수집 [!DNL SFTP]](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials)에 대한 안내서를 참조하십시오.

![SSH 공개 키를 사용하는 SFTP 원본에 대한 새 계정 화면입니다.](../../../../images/tutorials/create/sftp/ssh.png)

>[!ENDTABS]

## 다음 단계

이 자습서에 따라 SFTP 계정에 대한 연결을 설정했습니다. 이제 다음 자습서를 계속 진행하고 [클라우드 저장소에서 Experience Platform으로 데이터를 가져오도록 데이터 흐름을 구성](../../dataflow/batch/cloud-storage.md)할 수 있습니다.
