---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: UI에서 Azure Data Lake Storage Gen2 원본 커넥터 만들기
topic: overview
translation-type: tm+mt
source-git-commit: dd036cf4df5d772206d2b73292c60f2d866ba0de
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 1%

---


# UI에서 [!DNL Azure Data Lake Storage Gen2] 소스 커넥터 만들기

Adobe Experience Platform의 소스 커넥터는 예약된 기준으로 외부 소스 데이터를 인제스트하는 기능을 제공합니다. 이 자습서에서는 [!DNL Azure Data Lake Storage Gen2] 사용자 인터페이스를 사용하여 소스 커넥터(이하 &quot;[!DNL ADLS Gen2][!DNL Platform] &quot;라 한다)를 인증하는 단계를 제공합니다.

## 시작하기

이 자습서에서는 다음 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

- [[!DNL Experience Data Model] (XDM) 시스템](../../../../../xdm/home.md):고객 경험 데이터를 [!DNL Experience Platform] 구성하는 표준화된 프레임워크
   - [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md):스키마 컴포지션의 주요 원칙 및 모범 사례 등 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   - [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md):스키마 편집기 UI를 사용하여 사용자 정의 스키마를 생성하는 방법을 알아봅니다.
- [[!DNL 실시간 고객 프로필]](../../../../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 유효한 ADLS Gen2 연결이 있는 경우 이 문서의 나머지 부분을 건너뛰고 데이터 흐름 [구성에 대한 자습서로 진행할 수 있습니다](../../dataflow/batch/cloud-storage.md).

### 필요한 자격 증명 수집

소스 커넥터를 인증하려면 [!DNL ADLS Gen2] 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `url` | 끝점입니다 [!DNL ADLS Gen2]. |
| `servicePrincipalId` | 응용 프로그램의 클라이언트 ID입니다. |
| `servicePrincipalKey` | 응용 프로그램 키 |
| `tenant` | 응용 프로그램이 포함된 테넌트 정보. |

이러한 값에 대한 자세한 내용은 이 문서 [ [!DNL ADLS Gen2] 를 참조하십시오](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage).

## 계정 [!DNL ADLS Gen2] 연결

필요한 자격 증명을 수집했으면 아래 절차에 따라 [!DNL ADLS Gen2] 계정을 연결하여 연결할 수 있습니다 [!DNL Platform].

[Adobe Experience Platform](https://platform.adobe.com) 에 로그인한 다음 **** 왼쪽 탐색 막대에서 소스를 선택하여 **[!UICONTROL 소스 작업 영역에]** 액세스합니다. [ **[!UICONTROL 카탈로그]** ] 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면의 왼쪽에 있는 카탈로그에서 해당 범주를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

데이터베이스 **[!UICONTROL 카테고리]** 아래에서 **[!UICONTROL Azure Data Lake Gen2를]**&#x200B;선택합니다. 이 커넥터를 처음 사용하는 경우 구성을 **[!UICONTROL 선택합니다]**. 그렇지 않은 경우 데이터 **[!UICONTROL 추가를]** 선택하여 새 ADLS Gen2 커넥터를 만듭니다.

![](../../../../images/tutorials/create/adls-gen2/catalog.png)

Azure **[!UICONTROL Data Lake Gen2에 연결]** 대화 상자가 나타납니다. 이 페이지에서 새 자격 증명이나 기존 자격 증명을 사용할 수 있습니다.

### 새 계정

새 자격 증명을 사용하는 경우 새 계정 **[!UICONTROL 을 선택합니다]**. 표시되는 입력 양식에서 이름, 선택적 설명 및 자격 증명을 [!DNL ADLS Gen2] 제공합니다. 완료되면 **[!UICONTROL Connect를]** 선택한 다음 새 연결이 설정될 때까지 잠시 기다립니다.

![](../../../../images/tutorials/create/adls-gen2/connect.png)

### 기존 계정

기존 계정을 연결하려면 연결할 [!DNL ADLS Gen2] 계정을 선택한 다음 **[!UICONTROL 다음을]** 선택하여 진행합니다.

![](../../../../images/tutorials/create/adls-gen2/existing.png)

## 다음 단계

이 튜토리얼을 따라 계정에 대한 연결을 설정해 [!DNL ADLS Gen2] 드렸습니다. 이제 다음 튜토리얼로 계속 진행하여 데이터 흐름 [을 구성하여 클라우드 스토리지의 데이터를 [!DNL Platform]](../../dataflow/batch/cloud-storage.md)가져올 수 있습니다.