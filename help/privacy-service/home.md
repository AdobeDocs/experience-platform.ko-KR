---
keywords: Experience Platform;홈;인기 항목;GDPR;gdpr;ccpa:CCPA;PDPA;PDPA;pdpa_that;PDPA_THA;lgpd;LGPD;lgpd_bra;LGPD_BRA;
solution: Experience Platform
title: Privacy Service 개요
description: Privacy Service을 사용하면 Experience Cloud 데이터 작업에서 법적 개인정보 보호 규정을 자동으로 준수할 수 있습니다.
exl-id: 585f7619-5072-413b-9a62-be0ea0cd4d1b
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1389'
ht-degree: 6%

---

# [!DNL Privacy Service] 개요

더 나은 고객 경험을 게재하려면 고객의 개인 데이터를 수집하고 저장해야 합니다. 이 데이터를 사용할 때는 고객의 개인 정보를 이해하고 존중하는 것이 중요합니다. 새로운 법률 및 조직 규정은 사용자가 요청 시 데이터 저장소에서 개인 데이터를 액세스하거나 삭제할 수 있는 권한을 제공합니다.

Adobe Experience Platform [!DNL Privacy Service] 는 비즈니스가 고객의 개인 데이터를 관리하는 데 필요한 방식의 근본적인 변화에 따라 개발되었습니다. 의 주요 목적 [!DNL Privacy Service] 는 데이터 개인정보 보호 규정 준수를 자동화하며, 이를 위반할 경우 심각한 벌금이 부과되고 비즈니스의 데이터 운영에 지장을 줄 수 있습니다.

[!DNL Privacy Service] 는 고객 데이터 요청을 관리하는 데 도움이 되는 RESTful API 및 사용자 인터페이스를 제공합니다. 포함 [!DNL Privacy Service], Adobe Experience Cloud 애플리케이션에서 개인 고객 데이터에 액세스하고 삭제하도록 요청을 제출할 수 있으므로 법적 및 조직의 개인 정보 보호 규정을 자동으로 준수할 수 있습니다.

## 시작하기 [!DNL Privacy Service] {#getting-started}

를 사용하기 위하여 [!DNL Privacy Service], 조직의 개인 정보 보호 요구 사항, 고객으로부터 수집하는 id 데이터의 종류 및 CRM 시스템과 서비스를 연결하는 최상의 방법 측면에서 몇 가지 주요 의사 결정을 내려야 합니다.

이러한 결정은 다음과 같은 질문을 통해 요약할 수 있습니다.

1. **고객들로부터 어떤 정보를 수집하고 있습니까?**
   * 를 최대한 활용하려면 [!DNL Privacy Service]를 사용하려면 고객으로부터 수집하는 데이터의 유형과 개인정보 보호 규정의 적용 대상을 자세히 이해해야 합니다. 의 섹션을 참조하십시오. [개인 정보 보호 요구 사항 확인](#requirements) 추가 정보.
1. **데이터에 올바른 레이블을 지정했습니까?**
   * 서비스에서 개인 정보 보호 작업 중에 액세스하거나 삭제할 필드를 결정하려면 데이터에 올바른 레이블을 지정해야 합니다. 의 섹션을 참조하십시오. [레이블 지정 데이터](#label) 추가 정보.
1. **보낼 ID를 알고 있습니까 [!DNL Privacy Service]?**
   * 개인 정보 보호 요청을 보낼 때 특정 Adobe 애플리케이션과 관련된 개별 고객 ID를 제공해야 합니다. 의 섹션을 참조하십시오. [id 데이터 제공](#identity)  및 [개인 정보 보호 요청 만들기](#requests) 추가 정보.
1. **개인 정보 보호 작업을 추적하는 방법**
   * 개인 정보 보호 요청을 수행하면 상태 및 결과를 추적하는 몇 가지 옵션이 있습니다. 의 섹션을 참조하십시오. [개인 정보 작업 모니터링](#monitor) 추가 정보.

아래 섹션에서는 이러한 중요한 전제 조건 단계에 대한 일반적인 지침을 제공하고 추가 단계에 대한 링크도 제공합니다 [!DNL Privacy Service] 자세한 내용은 설명서 를 참조하십시오.

### 조직의 개인 정보 보호 요구 사항 결정 {#requirements}

비즈니스의 성격과 운영되는 관할 구역에 따라 데이터 운영에 법적 개인 정보 보호 규정이 적용될 수 있습니다. 이러한 규정에서는 고객에게 수집된 데이터에 대한 액세스를 요청할 수 있는 권한과 저장된 데이터의 삭제를 요청할 수 있는 권한을 부여하는 경우가 많습니다. 설명서 전체에서 개인 데이터에 대한 이러한 고객 요청을 &quot;개인 정보 보호 요청&quot;이라고 합니다.

다음과 같은 다양한 법적 개인 정보 보호 규정에 대한 자세한 내용 [!DNL Privacy Service] 자주 묻는 질문에 대한 주요 용어 및 답변을 포함하여 의 요청을 관리합니다. [개인 정보 보호 규정 문서](./regulations/overview.md).

데이터 작업이 지원되는 규정의 목적에 해당하는 경우 해당 설명서를 검토하여 고객에게 제공되는 특정 개인 정보 보호 권한 및 개인 정보 보호 요청을 준수하기 위한 규정 준수 창과 같은 중요한 정보를 확인하십시오. 통합 방법을 결정할 때 이 정보를 고려해야 합니다 [!DNL Privacy Service] 를 crm 시스템에 추가하여 고객이 웹 사이트와 상호 작용하여 개인 정보 요청을 하는 방법에 대해 알아봅니다.

이러한 결정을 내릴 때는 법적 규정 외에도 조직에 적용되는 조직 또는 업계 표준도 고려해야 합니다.

### 개인 정보 보호 요청에 대한 레이블 데이터 {#label}

에 따라 [!DNL Experience Cloud] 사용 중인 응용 프로그램에서는 개인 정보 보호 요청에 대한 응답으로 액세스하거나 삭제해야 하는 특정 데이터 필드에 레이블을 지정해야 합니다. 데이터에 레이블을 지정하는 프로세스는 애플리케이션마다 다릅니다. 지원되는 각 Adobe 애플리케이션에 대한 데이터에 레이블을 지정하는 방법을 알아보려면 다음의 문서를 참조하십시오. [Experience Cloud 애플리케이션](./experience-cloud-apps.md).

### 전송할 ID 데이터 유형 확인 [!DNL Privacy Service] {#identity}

주문 [!DNL Privacy Service] 고객의 개인 정보 보호 요청을 처리하려면 요청 자체에 해당 고객에 대한 하나 이상의 고유 id 값을 제공해야 합니다. 고유 ID 값은 개인 및 사용자 내에 저장된 개인 데이터를 식별하는 데 사용할 수 있는 모든 정보입니다 [!DNL Experience Cloud] 데이터 저장소입니다. [!DNL Privacy Service] 은 이 id 정보를 사용하여 요청의 특성(액세스, 삭제 또는 옵트아웃)에 따라 고객의 개인 데이터를 찾고 처리합니다.

에 따라 [!DNL Experience Cloud] crm 시스템에서 사용하는 응용 프로그램에는 각 고객에 대해 제공해야 하는 id 값의 유형과 개수가 달라집니다. 일부 애플리케이션은 자체 내부 고객 ID 값(예: Adobe Target ID)을 활용하는 반면 다른 솔루션은 Adobe의 글로벌 식별자를 사용합니다 [!DNL Experience Cloud Identity Service] (ECID) 모든 항목에서 고객 활동을 추적하는 [!DNL Experience Cloud] 응용 프로그램. 또한 이메일 주소나 전화번호와 같은 일반적인 개인 정보도 유효한 신원 데이터로 기능할 수 있습니다.

의 문서 [개인 정보 보호 요청에 대한 id 데이터](./identity-data.md) 은 허용되는 id 정보 유형에 대해 보다 자세한 정보를 제공합니다 [!DNL Privacy Service]. 또한 이 문서에서는 Adobe 기술을 활용하여 고객이 웹 사이트와 상호 작용할 때 고객의 적절한 ID 정보를 효과적으로 검색하고 해당 데이터를 로 전송하는 방법에 대한 지침을 제공합니다 [!DNL Privacy Service] API 요청.

### 개인 정보 보호 요청 시작 {#requests}

비즈니스의 개인 정보 보호 요구 사항을 결정하고 전송할 ID 값을 결정했으면 [!DNL Privacy Service], 개인 정보 보호 요청을 시작할 수 있습니다. [!DNL Privacy Service] 에서는 API 또는 UI를 통해 개인 정보 보호 요청을 보낼 수 있습니다.

>[!IMPORTANT]
>
>아래 섹션에서는 API 또는 UI에서 일반적인 개인 정보 요청을 하는 방법을 다루는 설명서에 대한 링크를 제공합니다. 그러나 다음에 따라 [!DNL Experience Cloud] 사용 중인 응용 프로그램에서 요청 페이로드로 보내야 하는 필드가 이 안내서에 표시된 예와 다를 수 있습니다.
>
>API 또는 UI 안내서와 함께 따라가면서 다음 문서를 참조하십시오. [Privacy Service 및 Experience Cloud 애플리케이션](./experience-cloud-apps.md) 특정 사용자에 대한 개인 정보 보호 요청을 포맷하는 방법에 대한 추가 설명서 [!DNL Experience Cloud] 애플리케이션.
>
>개인 정보 보호 요청은 Experience Cloud 애플리케이션 간에 비동기적으로 처리됩니다. Privacy Service이 요청을 수신하면 각 애플리케이션이 요청을 완료하는 데 몇 분에서 몇 주 정도 걸릴 수 있습니다. 각 요청을 완료하는 데 걸리는 시간은 작업 중인 애플리케이션과 처리해야 하는 데이터의 양에 따라 다릅니다.

#### API 사용

다음 [[!DNL Privacy Service API]](https://www.adobe.io/experience-platform-apis/references/privacy-service/) 은 RESTful API 호출을 사용하여 개인 정보 보호 작업을 만들고 관리하기 위한 몇 가지 끝점을 제공하여 의 개인 정보 보호 규정 준수에 프로그래밍 방식으로 접근할 수 있도록 합니다. [!DNL Experience Cloud] 응용 프로그램. API 사용 방법에 대한 자세한 단계는 [Privacy Service API 안내서](api/overview.md).

#### UI 사용

>[!NOTE]
>
>다음 [!DNL Privacy Service] UI는 현재 액세스 및 삭제 요청만 지원합니다. 모든 옵트아웃 요청은 대신 API를 통해 수행해야 합니다.

다음 [!DNL Privacy Service] UI를 사용하면 그래픽 인터페이스를 사용하여 개인 정보 작업을 만들고 모니터링할 수 있습니다. UI에는 **[!UICONTROL 상태 보고서]** 모든 활성 요청의 상태를 시각적으로 표시하고 기본 기능을 사용하여 새 요청을 만들 수 있는 위젯 **[!UICONTROL 요청 빌더]** 또는 JSON 파일을 업로드하여 검색할 수 있습니다. UI 사용에 대한 자세한 내용은 [Privacy Service 사용 안내서](ui/overview.md).

### 개인 정보 작업 모니터링 {#monitor}

개인 정보 작업을 완료하면 상태 및 결과를 모니터링하기 위한 몇 가지 옵션이 제공됩니다.

| 모니터링 방법 | 설명 |
| --- | --- |
| [!DNL Privacy Service] UI | 다음 [!DNL Privacy Service] UI는 모든 활성 요청의 상태를 시각적으로 표시할 수 있는 모니터링 대시보드를 제공합니다. 다음을 참조하십시오. [Privacy Service 사용 안내서](ui/overview.md) 추가 정보. |
| [!DNL Privacy Service] API | 에서 제공한 조회 끝점을 사용하여 개인 정보 보호 작업의 상태를 프로그래밍 방식으로 모니터링할 수 있습니다. [!DNL Privacy Service] API. 다음을 참조하십시오. [Privacy Service API 안내서](./api/overview.md) api 사용 방법에 대한 자세한 단계입니다. |
| [!DNL Privacy Events] | [!DNL Privacy Events] 구성된 웹후크로 전송된 Adobe I/O 이벤트를 활용하여 효율적인 작업 요청 자동화를 꾀할 수 있습니다. 또한 폴링을 수행할 필요가 줄어들거나 없어집니다. [!DNL Privacy Service] 작업이 완료되었는지 또는 워크플로우 내의 특정 이정표에 도달했는지 확인하기 위한 API입니다. 다음 튜토리얼 참조: [개인 정보 이벤트에 가입](./privacy-events.md) 추가 정보. |

## 다음 단계

이 문서는 다음에 대한 높은 수준의 개요를 제공했습니다. [!DNL Privacy Service] 및 서비스 기능을 사용하기 시작하는 데 필요한 주요 단계입니다. 작업의 다양한 측면에 대한 자세한 내용은 개요 전체에 연결된 설명서를 참조하십시오 [!DNL Privacy Service].
