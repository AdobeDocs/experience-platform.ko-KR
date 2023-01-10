---
keywords: Experience Platform;홈;인기 항목;FTP;ftp
solution: Experience Platform
title: UI에서 FTP 소스 연결 만들기
type: Tutorial
description: Adobe Experience Platform UI를 사용하여 FTP 소스 연결을 만드는 방법을 알아봅니다.
exl-id: 8e505ead-4bae-43fe-830b-75620e8fba28
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 1%

---

# UI에서 FTP 소스 연결 만들기

>[!NOTE]
>
>FTP 커넥터는 베타에 있습니다. 자세한 내용은 [소스 개요](../../../../home.md#terms-and-conditions) 베타 레이블이 지정된 커넥터 사용에 대한 자세한 정보.

이 자습서에서는 Adobe Experience Platform UI를 사용하여 FTP 소스 연결을 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 작성 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 빌딩 블록에 대해 알아봅니다.
   * [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아보십시오.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 유효한 FTP 연결이 있는 경우 이 문서의 나머지 부분을 건너뛰고 다음 방법으로 자습서를 진행할 수 있습니다. [데이터 흐름 구성](../../dataflow/batch/cloud-storage.md).

### 필요한 자격 증명 수집

FTP에 연결하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `host` | FTP 서버와 연결된 이름 또는 IP 주소입니다. |
| `username` | FTP 서버에 액세스할 수 있는 사용자 이름입니다. |
| `password` | FTP 서버의 암호입니다. |

## FTP 서버에 연결

필요한 자격 증명을 수집했으면 아래 단계에 따라 Platform에 연결할 새 FTP 계정을 만들 수 있습니다.

에 로그인합니다. [Adobe Experience Platform](https://platform.adobe.com) 그런 다음 **[!UICONTROL 소스]** 왼쪽 탐색 모음에서 를 클릭하여 [!UICONTROL 소스] 작업 공간. 다음 [!UICONTROL 카탈로그] 화면에는 로 인바운드 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래에 [!UICONTROL 클라우드 스토리지] 카테고리, 선택 **[!UICONTROL FTP]**. 이 커넥터를 처음 사용하는 경우 **[!UICONTROL 구성]**. 그렇지 않으면 을 선택합니다. **[!UICONTROL 데이터 추가]** 새 FTP 연결을 만듭니다 .

![카탈로그](../../../../images/tutorials/create/ftp/catalog.png)

다음 **[!UICONTROL FTP에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 새 계정

새 자격 증명을 사용하는 경우 **[!UICONTROL 새 계정]**. 표시되는 입력 양식에서 이름, 선택적 설명 및 자격 증명을 제공합니다. 완료되면 을 선택합니다 **[!UICONTROL Connect]** 그런 다음 새 연결이 설정될 시간을 허용합니다.

![새](../../../../images/tutorials/create/ftp/new.png)

### 기존 계정

기존 계정을 연결하려면 연결할 FTP 계정을 선택한 다음 을(를) 선택합니다 **[!UICONTROL 다음]** 계속 진행합니다.

![기존](../../../../images/tutorials/create/ftp/existing.png)

## 다음 단계

이 자습서를 따라 FTP 계정에 대한 연결을 설정했습니다. 이제 다음 자습서를 계속 진행하고 [클라우드 저장소에서 플랫폼으로 데이터를 가져오도록 데이터 흐름 구성](../../dataflow/batch/cloud-storage.md).
