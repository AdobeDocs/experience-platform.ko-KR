---
keywords: Experience Platform;홈;인기 항목;Azure Data Lake Storage Gen2;ADLS Gen2;adls gen2;adls 커넥터
solution: Experience Platform
title: UI에서 Azure Data Lake Storage Gen2 Source 연결 만들기
type: Tutorial
description: Adobe Experience Platform UI를 사용하여 Azure Data Lake Storage Gen2 소스 연결을 만드는 방법을 알아봅니다.
exl-id: d81b7593-08a3-43f8-a8bc-f5547a6cd55a
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 2%

---

# UI에서 [!DNL Azure Data Lake Storage Gen2] 소스 연결 만들기

Adobe Experience Platform의 Source 커넥터는 일정에 따라 외부 소스 데이터를 수집하는 기능을 제공합니다. 이 자습서에서는 [!DNL Experience Platform] 사용자 인터페이스를 사용하여 [!DNL Azure Data Lake Storage Gen2]&#x200B;(이하 &quot;[!DNL ADLS Gen2]&quot;) 원본 커넥터를 인증하는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

- [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): [!DNL Experience Platform]에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   - [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   - [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아봅니다.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 유효한 ADLS Gen2 연결이 있는 경우 이 문서의 나머지 부분을 건너뛰고 [데이터 흐름 구성](../../dataflow/batch/cloud-storage.md)에 대한 자습서로 진행할 수 있습니다.

### 필요한 자격 증명 수집

[!DNL ADLS Gen2] 원본 커넥터를 인증하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `url` | [!DNL ADLS Gen2]의 끝점입니다. |
| `servicePrincipalId` | 애플리케이션의 클라이언트 ID. |
| `servicePrincipalKey` | 애플리케이션 키. |
| `tenant` | 애플리케이션이 포함된 테넌트 정보입니다. |

이러한 값에 대한 자세한 내용은 [이 [!DNL ADLS Gen2] 문서](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage)를 참조하세요.

## [!DNL ADLS Gen2] 계정 연결

필요한 자격 증명을 수집했으면 아래 단계에 따라 [!DNL ADLS Gen2] 계정을 연결하여 [!DNL Experience Platform]에 연결할 수 있습니다.

[Adobe Experience Platform](https://platform.adobe.com)에 로그인한 다음 왼쪽 탐색 막대에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 **[!UICONTROL 소스]** 작업 영역에 액세스합니다. **[!UICONTROL 카탈로그]** 화면에 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

**[!UICONTROL 데이터베이스]** 범주에서 **[!UICONTROL Azure 데이터 레이크 Gen2]**&#x200B;을(를) 선택합니다. 이 커넥터를 처음 사용하는 경우 **[!UICONTROL 구성]**&#x200B;을 선택하세요. 그렇지 않으면 **[!UICONTROL 데이터 추가]**&#x200B;를 선택하여 새 ADLS Gen2 커넥터를 만드십시오.

![](../../../../images/tutorials/create/adls-gen2/catalog.png)

**[!UICONTROL Azure Data Lake Gen2에 연결]** 대화 상자가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 새 계정

새 자격 증명을 사용하는 경우 **[!UICONTROL 새 계정]**&#x200B;을(를) 선택하십시오. 표시되는 입력 양식에서 이름, 선택적 설명 및 [!DNL ADLS Gen2] 자격 증명을 제공합니다. 완료되면 **[!UICONTROL 연결]**&#x200B;을 선택한 다음 새 연결을 설정할 시간을 허용합니다.

![](../../../../images/tutorials/create/adls-gen2/connect.png)

### 기존 계정

기존 계정에 연결하려면 연결할 [!DNL ADLS Gen2] 계정을 선택한 후 **[!UICONTROL 다음]**&#x200B;을(를) 선택하여 계속하십시오.

![](../../../../images/tutorials/create/adls-gen2/existing.png)

## 다음 단계

이 자습서에 따라 [!DNL ADLS Gen2] 계정에 대한 연결을 설정했습니다. 이제 다음 자습서를 계속 진행하고 [클라우드 저장소에서  [!DNL Experience Platform]](../../dataflow/batch/cloud-storage.md)(으)로 데이터를 가져오도록 데이터 흐름을 구성할 수 있습니다.
