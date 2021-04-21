---
keywords: Experience Platform;홈;인기 항목;GDPR;GDPR;GDPA;PDPA;PDPA;PDPA_that;PDPA_THA;LGPD;LGPD_bra;LGPD_LGPD_BRA;
solution: Experience Platform
title: Privacy Service 개요
topic-legacy: overview
description: Privacy Service을 사용하면 Experience Cloud 데이터 작업에서 법률 개인 정보 보호 규정을 자동으로 준수할 수 있습니다.
exl-id: 585f7619-5072-413b-9a62-be0ea0cd4d1b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1390'
ht-degree: 0%

---

# [!DNL Privacy Service] 개요

더 나은 고객 경험을 제공하기 위해서는 고객의 개인 데이터를 수집하고 저장해야 합니다. 이 데이터를 사용할 때는 고객의 개인 정보를 이해하고 존중해야 합니다. 새로운 법률 및 조직 규정은 사용자가 요청 시 데이터 저장소에서 개인 데이터를 액세스하거나 삭제할 수 있는 권한을 제공합니다.

Adobe Experience Platform [!DNL Privacy Service]은(는) 비즈니스가 고객의 개인 데이터를 관리하는 데 필요한 기본적인 변화에 대응하여 개발되었습니다. [!DNL Privacy Service]의 주된 목적은 데이터 개인 정보 보호 규정 준수를 자동화하는 것입니다. 이러한 규정을 위반하면 엄청난 벌금을 내고 비즈니스 데이터 작업을 방해할 수 있습니다.

[!DNL Privacy Service] 고객 데이터 요청을 관리하는 데 도움이 되는 RESTful API 및 사용자 인터페이스를 제공합니다. [!DNL Privacy Service]을 사용하면 Adobe Experience Cloud 애플리케이션에서 개인 고객 데이터를 액세스하고 삭제하기 위한 요청을 제출할 수 있으므로 법적 및 조직의 개인 정보 보호 규정을 자동으로 준수할 수 있습니다.

## [!DNL Privacy Service] {#getting-started} 시작하기

[!DNL Privacy Service]을(를) 사용하려면 조직의 개인정보 보호 요구 사항, 고객으로부터 수집하는 ID 데이터의 종류, CRM 시스템과 서비스를 연계하는 최상의 방법 등 몇 가지 주요 결정을 내려야 합니다.

이러한 결정은 다음 질문으로 요약할 수 있습니다.

1. **고객으로부터 어떤 정보를 수집하고 있습니까?**
   * [!DNL Privacy Service]을(를) 최대한 활용하려면 고객으로부터 수집하는 데이터의 유형과 수집 중 어떤 것이 개인 정보 보호 규정에 따르는지 자세히 이해해야 합니다. 자세한 내용은 [개인정보 보호 요구 사항](#requirements)에 대한 섹션을 참조하십시오.
1. **데이터에 레이블을 올바로 지정했습니까?**
   * 서비스에서 개인 정보 작업 중에 액세스하거나 삭제할 필드를 결정하려면 데이터에 적절히 레이블을 지정해야 합니다. 자세한 내용은 [레이블 지정 데이터](#label)의 섹션을 참조하십시오.
1. **보낼 ID를 알고  [!DNL Privacy Service]있습니까?**
   * 개인 정보 요청을 전송할 때 특정 Adobe 응용 프로그램별 개별 고객 ID를 제공해야 합니다. 자세한 내용은 [ID 데이터 제공](#identity) 및 [개인 정보 보호 요청](#requests)의 섹션을 참조하십시오.
1. **개인 정보 보호 작업을 어떻게 추적합니까?**
   * 개인 정보를 요청하면 상태와 결과를 추적할 수 있는 여러 옵션이 있습니다. 자세한 내용은 [개인 정보 작업 모니터링](#monitor)의 섹션을 참조하십시오.

아래 섹션에서는 이러한 중요한 사전 요구 사항 단계에 대한 일반적인 지침을 제공하며 자세한 내용은 추가 [!DNL Privacy Service] 설명서에 대한 링크를 제공합니다.

### 조직의 개인 정보 요구 사항 확인 {#requirements}

비즈니스의 성격과 해당 기관이 운영하는 사법권에 따라 데이터 운영에 법적 개인정보 보호 규정이 적용될 수 있습니다. 이러한 규정은 귀하로부터 수집한 데이터에 대한 액세스를 요청할 수 있는 권한과 저장된 데이터의 삭제를 요청하는 권한을 고객에게 부여합니다. 이러한 고객의 개인 데이터에 대한 요청은 문서 전체에서 &quot;개인 정보 보호 요청&quot;이라고 합니다.

[!DNL Privacy Service]이(가) 주요 약관 및 FAQ에 대한 답변을 포함하여 요청을 관리하는 다양한 법적 개인 정보 보호 규정에 대한 자세한 내용은 [개인 정보 보호 규정 문서](./regulations/overview.md)를 참조하십시오.

데이터 작업이 지원되는 모든 규정의 목적에 부합하는 경우 문서를 검토하여 고객에게 제공하는 특정 개인정보 보호 권리 및 개인 정보 보호 요청을 준수하기 위한 규정 준수 여부와 같은 중요한 정보를 검토하십시오. 이 정보는 [!DNL Privacy Service]을(를) CRM 시스템에 통합하는 방법 및 고객이 개인 정보 보호를 요청하기 위해 웹 사이트와 상호 작용하는 방법을 결정할 때 고려해야 합니다.

법적 규정 외에 조직에 적용되는 조직 또는 산업 표준도 이러한 결정을 내릴 때 고려해야 합니다.

### 개인 정보 요청에 대한 레이블 데이터 {#label}

사용 중인 응용 프로그램에 따라 개인 정보 요청에 응답하여 액세스하거나 삭제해야 하는 특정 데이터 필드에 레이블을 지정해야 합니다. [!DNL Experience Cloud] 데이터에 레이블을 지정하는 프로세스는 애플리케이션에 따라 다릅니다. 지원되는 각 Adobe 응용 프로그램의 데이터에 레이블을 지정하는 방법에 대해 알아보려면 [Experience Cloud 응용 프로그램](./experience-cloud-apps.md)의 문서를 참조하십시오.

### [!DNL Privacy Service] {#identity}(으)로 보낼 ID 데이터의 유형을 결정합니다.

[!DNL Privacy Service]이(가) 고객의 개인 정보 요청을 처리하려면 해당 고객에 대해 하나 이상의 고유 ID 값을 요청 자체에 제공해야 합니다. 고유 ID 값은 [!DNL Experience Cloud] 데이터 저장소 내에서 개인 및 저장된 개인 데이터를 식별하는 데 사용할 수 있는 모든 정보입니다. [!DNL Privacy Service] 이 id 정보를 사용하여 요청의 특성에 따라 고객의 개인 데이터를 찾아 처리합니다(액세스, 삭제 또는 수신 거부).

CRM 시스템에서 사용하는 [!DNL Experience Cloud] 응용 프로그램에 따라 각 고객에게 제공해야 하는 ID 값의 유형과 수가 달라집니다. 일부 응용 프로그램은 자체 내부 고객 ID 값(예: Adobe Target ID)을 사용하는 반면 다른 솔루션은 모든 [!DNL Experience Cloud] 응용 프로그램에서 고객 활동을 추적하는 Adobe [!DNL Experience Cloud Identity Service](ECID)의 글로벌 식별자를 사용합니다. 또한 이메일 주소 또는 전화 번호와 같은 일반적인 개인 정보도 유효한 ID 데이터가 될 수 있습니다.

[개인 정보 요청에 대한 ID 데이터](./identity-data.md)에 있는 문서는 [!DNL Privacy Service]에 허용된 ID 정보 유형에 대한 자세한 정보를 제공합니다. 또한 이 문서에서는 Adobe 기술을 활용하여 고객이 웹 사이트와 상호 작용할 때 고객으로부터 적절한 ID 정보를 효과적으로 검색하고 API 요청의 [!DNL Privacy Service]으로 해당 데이터를 전송하는 방법에 대한 지침도 제공합니다.

### 개인 정보 요청 만들기 시작 {#requests}

비즈니스 개인 정보 요구 사항을 결정하고 [!DNL Privacy Service]에 보낼 ID 값을 결정하면 개인 정보 요청을 시작할 수 있습니다. [!DNL Privacy Service] API 또는 UI를 통해 개인 정보 요청을 전송할 수 있도록 해줍니다.

>[!IMPORTANT]
>
>아래 섹션에서는 API 또는 UI에서 일반적인 개인정보 보호 요청을 수행하는 방법을 설명하는 설명서에 대한 링크를 제공합니다. 그러나 사용 중인 [!DNL Experience Cloud] 응용 프로그램에 따라 요청 페이로드에서 보내야 하는 필드는 이러한 안내서에 표시된 예제와 다를 수 있습니다.
>
>API 또는 UI 가이드와 함께 할 때 특정 [!DNL Experience Cloud] 애플리케이션에 대한 개인 정보 요청의 형식 지정 방법에 대한 자세한 내용은 [Privacy Service 및 Experience Cloud 응용 프로그램](./experience-cloud-apps.md)에 있는 문서를 참조하십시오.
>
>또한 개인 정보 요청은 Experience Cloud 응용 프로그램에서 비동기적으로 처리됩니다. Privacy Service에서 요청을 받으면 각 애플리케이션이 요청을 완료하는 데 몇 분에서 몇 주가 걸릴 수 있습니다. 각 요청을 완료하는 데 걸리는 시간은 작업 중인 응용 프로그램과 처리해야 하는 데이터의 양입니다.

#### API 사용

[[!DNL Privacy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml)은 RESTful API 호출을 사용하여 개인 정보 작업을 만들고 관리하기 위한 여러 끝점을 제공하므로 [!DNL Experience Cloud] 응용 프로그램에 대한 개인 정보 보호 규정 준수에 프로그래밍 방식으로 액세스할 수 있습니다. API 사용 방법에 대한 자세한 내용은 [Privacy Service API 개발자 안내서](api/getting-started.md)를 참조하십시오.

#### UI 사용

>[!NOTE]
>
>[!DNL Privacy Service] UI는 현재 액세스 및 삭제 요청만 지원합니다. 모든 옵트아웃 요청은 대신 API를 통해 해야 합니다.

[!DNL Privacy Service] UI를 사용하면 그래픽 인터페이스를 사용하여 개인 정보 작업을 만들고 모니터링할 수 있습니다. UI에는 모든 활성 요청의 상태를 시각적으로 표시하는 **[!UICONTROL Status Report]** 위젯이 포함되어 있으며, 내장 **[!UICONTROL Request Builder]**&#x200B;을 사용하거나 JSON 파일을 업로드하여 새 요청을 만들 수 있습니다. UI 사용에 대한 자세한 내용은 [Privacy Service 사용 안내서](ui/overview.md)를 참조하십시오.

### 개인 정보 작업 모니터링 {#monitor}

개인 정보 보호 작업을 수행한 후에는 상태 및 결과를 모니터링할 수 있는 여러 옵션이 있습니다.

| 모니터링 방법 | 설명 |
| --- | --- |
| [!DNL Privacy Service] UI | [!DNL Privacy Service] UI는 모든 활성 요청의 상태를 시각적으로 표시할 수 있는 모니터링 대시보드를 제공합니다. 자세한 내용은 [Privacy Service 사용 안내서](ui/overview.md)를 참조하십시오. |
| [!DNL Privacy Service] API | [!DNL Privacy Service] API에서 제공하는 조회 끝점을 사용하여 개인 정보 작업 상태를 프로그래밍 방식으로 모니터링할 수 있습니다. API 사용 방법에 대한 자세한 내용은 [Privacy Service 개발자 안내서](./api/getting-started.md)를 참조하십시오. |
| [!DNL Privacy Events] | [!DNL Privacy Events] 효율적인 작업 요청 자동화를 촉진하기 위해 구성된 웹 후크에 전송된 Adobe I/O 이벤트를 활용합니다. 작업이 완료되었는지 또는 워크플로우 내의 특정 이정표에 도달했는지 확인하기 위해 [!DNL Privacy Service] API를 폴링할 필요가 줄어들었습니다. 자세한 내용은 [개인정보 보호 이벤트 가입](./privacy-events.md)의 자습서를 참조하십시오. |

## 다음 단계

이 문서에서는 [!DNL Privacy Service]에 대한 수준 높은 개요와 서비스 기능 사용을 시작하는 데 필요한 주요 단계를 제공합니다. [!DNL Privacy Service]으로 작업하는 다양한 측면에 대한 자세한 내용은 개요 전체에 연결된 설명서를 참조하십시오.
