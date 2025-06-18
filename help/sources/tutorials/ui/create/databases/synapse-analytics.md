---
title: UI에서 Azure Synapse Analytics Source 연결 만들기
description: Adobe Experience Platform UI를 사용하여 Azure Synapse Analytics(이하 "Synapse") 소스 연결을 만드는 방법을 알아봅니다.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 1f1ce317-eaaf-4ad2-a5fb-236983220bd7
source-git-commit: f8eb8640360205e8ae9579d4b664d4880bf8a368
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# UI에서 [!DNL Azure Synapse Analytics] 소스 연결 만들기

>[!IMPORTANT]
>
>[!DNL Azure Synapse Analytics] 소스는 Real-Time Customer Data Platform Ultimate을 구매한 사용자가 소스 카탈로그에서 사용할 수 있습니다.

UI의 소스 작업 영역을 사용하여 [!DNL Azure Synapse Analytics] 계정을 Adobe Experience Platform에 연결하는 방법을 알아보려면 이 안내서를 참조하십시오.

## 시작

이 자습서에서는 Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): [!DNL Experience Platform]에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 올바른 [!DNL Azure Synapse Analytics] 연결이 있는 경우 이 문서의 나머지 부분을 건너뛰고 [데이터 흐름 구성](../../dataflow/databases.md)에 대한 자습서로 진행할 수 있습니다.

### 필요한 자격 증명 수집

인증에 대한 자세한 내용은 [[!DNL Azure Synapse Analytics] 개요](../../../../connectors/databases/synapse-analytics.md#prerequisites)를 읽어 보십시오.

## 소스 카탈로그 탐색

Experience Platform UI의 왼쪽 탐색에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 *[!UICONTROL 소스]* 작업 영역에 액세스합니다. 카테고리를 선택하거나 검색 창을 사용하여 소스를 찾습니다.

[!DNL Azure Synapse Analytics]에 연결하려면 *[!UICONTROL 데이터베이스]* 범주로 이동하여 **[!UICONTROL Azure Synapse 분석]** 소스 카드를 선택한 다음 **[!UICONTROL 설정]**&#x200B;을 선택하십시오.

>[!TIP]
>
>지정된 소스에 아직 인증된 계정이 없는 경우 소스 카탈로그의 소스에 **[!UICONTROL 설정]** 옵션이 표시됩니다. 인증된 계정을 만들면 이 옵션이 **[!UICONTROL 데이터 추가]**(으)로 변경됩니다.

![&quot;Azure Synapse Analytics&quot;가 있는 소스 카탈로그를 선택했습니다.](../../../../images/tutorials/create/azure-synapse-analytics/catalog.png)

## 기존 계정 사용 {#existing}

기존 계정을 사용하려면 **[!UICONTROL 기존 계정]**&#x200B;을(를) 선택한 다음 사용할 [!DNL Azure Synapse Analytics] 계정을 선택하십시오.

![원본 워크플로의 기존 계정 인터페이스입니다.](../../../../images/tutorials/create/azure-synapse-analytics/existing.png)

## 새 계정 만들기 {#new}

새 계정을 만들려면 **[!UICONTROL 새 계정]**&#x200B;을 선택한 다음 이름을 입력하고 필요에 따라 계정에 대한 설명을 추가하십시오.

![원본 워크플로의 새 계정 인터페이스입니다.](../../../../images/tutorials/create/azure-synapse-analytics/new.png)

### Experience Platform에 연결

계정 키 인증 또는 서비스 사용자 및 키 인증을 사용하여 [!DNL Azure Synapse Analytics] 계정을 Experience Platform에 연결할 수 있습니다.

>[!BEGINTABS]

>[!TAB 계정 키 인증]

계정 키 인증을 사용하려면 **[!UICONTROL 계정 키 인증]**&#x200B;을 선택하고 [연결 문자열](../../../../connectors/databases/synapse-analytics.md#prerequisites)을 제공한 다음 **[!UICONTROL 소스에 연결]**&#x200B;을 선택하십시오.

![&quot;계정 키 인증을 선택한 원본 워크플로의 &quot;새 계정 만들기&quot; 단계입니다.](../../../../images/tutorials/create/azure-synapse-analytics/account-key-auth.png)

>[!TAB 서비스 사용자 및 키 인증]

또는 **[!UICONTROL 서비스 사용자 및 키 인증]**&#x200B;을 선택하고 [인증 자격 증명](../../../../connectors/databases/synapse-analytics.md#prerequisites)에 대한 값을 제공한 다음 **[!UICONTROL 소스에 연결]**&#x200B;을 선택하십시오.

![소스 워크플로에서 &quot;서비스 사용자 및 키 인증&quot;을 선택한 &quot;새 계정 만들기&quot; 단계입니다.](../../../../images/tutorials/create/azure-synapse-analytics/service-principal.png)

>[!ENDTABS]

## [!DNL Azure Synapse Analytics] 데이터에 대한 데이터 흐름 만들기

[!DNL Azure Synapse Analytics] 데이터베이스를 연결했으므로 이제 [데이터 흐름을 만들고 데이터베이스에서 Experience Platform으로 데이터를 수집](../../dataflow/databases.md)할 수 있습니다.
