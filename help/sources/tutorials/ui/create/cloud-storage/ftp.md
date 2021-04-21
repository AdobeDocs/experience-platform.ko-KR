---
keywords: Experience Platform;홈;인기 항목;FTP;ftp
solution: Experience Platform
title: UI에서 FTP 소스 연결 만들기
topic-legacy: overview
type: Tutorial
description: Adobe Experience Platform UI를 사용하여 FTP 소스 연결을 만드는 방법을 알아봅니다.
exl-id: 8e505ead-4bae-43fe-830b-75620e8fba28
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# UI에서 FTP 소스 연결 만들기

>[!NOTE]
>
>FTP 커넥터가 베타에 있습니다. 베타 레이블이 지정된 커넥터 사용에 대한 자세한 내용은 [소스 개요](../../../../home.md#terms-and-conditions)를 참조하십시오.

이 자습서에서는 Adobe Experience Platform UI를 사용하여 FTP 소스 연결을 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md):Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md):스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 블록에 대해 알아봅니다.
   * [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md):스키마 편집기 UI를 사용하여 사용자 정의 스키마를 생성하는 방법을 알아봅니다.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

유효한 FTP 연결이 이미 있는 경우 이 문서의 나머지 부분을 건너뛰고 [데이터 흐름 구성](../../dataflow/batch/cloud-storage.md)에서 자습서로 진행할 수 있습니다.

### 필요한 자격 증명 수집

FTP에 연결하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `host` | FTP 서버와 연결된 이름 또는 IP 주소입니다. |
| `username` | FTP 서버에 액세스할 수 있는 사용자 이름입니다. |
| `password` | FTP 서버의 암호입니다. |

## FTP 서버에 연결

필요한 자격 증명을 수집했으면 아래 절차에 따라 플랫폼에 연결할 새 FTP 계정을 만들 수 있습니다.

[Adobe Experience Platform](https://platform.adobe.com)에 로그인한 다음 왼쪽 탐색 막대에서 **[!UICONTROL Sources]**&#x200B;를 선택하여 [!UICONTROL Sources] 작업 영역에 액세스합니다. [!UICONTROL Catalog] 화면에는 인바운드 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면의 왼쪽에 있는 카탈로그에서 적절한 범주를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

[!UICONTROL Cloud storage] 범주에서 **[!UICONTROL FTP]**&#x200B;을 선택합니다. 이 커넥터를 처음 사용하는 경우 **[!UICONTROL Configure]** 을 선택합니다. 그렇지 않은 경우 **[!UICONTROL Add data]**&#x200B;을 선택하여 새 FTP 연결을 만듭니다.

![카탈로그](../../../../images/tutorials/create/ftp/catalog.png)

**[!UICONTROL Connect to FTP]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명이나 기존 자격 증명을 사용할 수 있습니다.

### 새 계정

새 자격 증명을 사용 중인 경우 **[!UICONTROL New account]**&#x200B;을 선택합니다. 표시되는 입력 양식에서 이름, 선택적 설명 및 자격 증명을 제공합니다. 완료되면 **[!UICONTROL Connect]**&#x200B;을 선택한 다음 새 연결이 설정될 때까지 잠시 기다려 주십시오.

![new](../../../../images/tutorials/create/ftp/new.png)

### 기존 계정

기존 계정을 연결하려면 연결하려는 FTP 계정을 선택한 다음 계속하려면 **[!UICONTROL Next]**&#x200B;을 선택합니다.

![기존](../../../../images/tutorials/create/ftp/existing.png)

## 다음 단계

이 자습서를 따라 FTP 계정에 대한 연결을 설정했습니다. 이제 다음 튜토리얼을 계속 진행할 수 있으며 [데이터 흐름 구성을 통해 클라우드 스토리지의 데이터를 플랫폼](../../dataflow/batch/cloud-storage.md)으로 가져올 수 있습니다.
