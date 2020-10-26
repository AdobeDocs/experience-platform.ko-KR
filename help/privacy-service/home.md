---
keywords: Experience Platform;home;popular topics;GDPR;gdpr;ccpa:CCPA;pdpa;PDPA;pdpa_that;PDPA_THA;lgpd;LGPD;lgpd_bra;LGPD_BRA;
solution: Experience Platform
title: Adobe Experience Platform Privacy Service
topic: overview
translation-type: tm+mt
source-git-commit: f3872d433949e6c14c28c6833b8498d4d01b8de3
workflow-type: tm+mt
source-wordcount: '1627'
ht-degree: 2%

---


# Adobe Experience Platform [!DNL Privacy Service] overview

더 나은 고객 경험을 제공하기 위해서는 고객의 개인 데이터를 수집 및 저장해야 합니다. 이 데이터를 사용하는 경우 고객의 개인 정보를 이해하고 존중해야 합니다. 새로운 법률 및 조직 규정은 사용자가 요청 시 데이터 저장소에서 개인 데이터를 액세스하거나 삭제할 수 있는 권한을 제공합니다.

Adobe Experience Platform [!DNL Privacy Service] 는 기업이 고객의 개인 정보를 관리하는 데 필요한 기본적인 변화에 대응하여 개발되었습니다. 데이터 개인 정보 보호 규정 준수를 자동화하는 [!DNL Privacy Service] 것이 가장 큰 목표이며, 이를 위반하면 엄청난 벌금이 부과되고 비즈니스 데이터 운영을 방해할 수 있습니다.

[!DNL Privacy Service] 고객 데이터 요청을 관리하는 데 도움이 되는 RESTful API 및 사용자 인터페이스를 제공합니다. 이 [!DNL Privacy Service]를 통해 Adobe Experience Cloud 애플리케이션에서 개인 고객 데이터를 액세스하고 삭제하라는 요청을 제출할 수 있으므로 법률 및 조직의 개인 정보 보호 규정을 자동으로 준수할 수 있습니다.

## Getting started with [!DNL Privacy Service] {#getting-started}

이를 활용하려면 조직의 개인 정보 [!DNL Privacy Service]요구 사항, 고객이 수집하는 ID 데이터의 종류, CRM 시스템과 서비스를 연결하는 최상의 방법 등 몇 가지 주요 결정을 내려야 합니다.

이러한 결정은 다음 질문으로 요약될 수 있습니다.

1. **고객으로부터 어떤 정보를 수집하고 있습니까?**
   * 최상의 사용 방법을 [!DNL Privacy Service]얻으려면 고객으로부터 수집하는 데이터의 유형과 그 중 어떤 데이터가 개인 정보 보호 규정에 위반되는지 자세히 파악해야 합니다. 자세한 내용은 개인 정보 요구 [사항](#requirements) 결정 섹션을 참조하십시오.
1. **데이터 레이블이 올바르게 지정되었습니까?**
   * 서비스에서 개인 정보 작업 중에 액세스하거나 삭제할 필드를 결정하려면 데이터 레이블이 적절하게 지정되어 있어야 합니다. 자세한 내용은 데이터 [레이블 지정](#label) 섹션을 참조하십시오.
1. **보낼 ID를 알고 있습니까 [!DNL Privacy Service]?**
   * 개인 정보 요청을 전송할 때는 특정 Adobe 응용 프로그램별 개별 고객 ID를 제공해야 합니다. 자세한 내용은 ID 데이터 [제공](#identity) 및 개인 정보 [요청](#requests) 에 대한 섹션을 참조하십시오.
1. **개인 정보 보호 작업은 어떻게 추적합니까?**
   * 개인 정보를 요청하면 해당 상태와 결과를 추적할 수 있는 여러 가지 옵션이 있습니다. 자세한 내용은 개인 정보 작업 [모니터링에](#monitor) 대한 섹션을 참조하십시오.

아래 섹션에서는 이러한 중요한 사전 요구 사항 단계에 대한 일반적인 지침을 제공하고 자세한 내용은 추가 [!DNL Privacy Service] 설명서에 대한 링크를 제공합니다.

### 조직의 개인 정보 보호 요구 사항 확인 {#requirements}

비즈니스의 성격과 해당 기관이 운영하는 관할지에 따라, 데이터 운영에 법적 개인정보 보호 규정이 적용될 수 있습니다. 이러한 규정은 고객이 수집한 데이터에 대한 액세스 권한을 요청할 수 있는 권한과 저장된 데이터의 삭제를 요청하는 권한을 부여합니다. 이러한 고객의 개인 데이터 요청은 문서 전체에서 &quot;개인 정보 요청&quot;이라고 합니다.

다음 표에서는 자세한 정보를 보려면 설명서에 대한 링크를 포함하여 요청을 [!DNL Privacy Service] 관리하는 법적 개인 정보 보호 규정에 대해 설명합니다.

| 규정 | 설명 |
| --- | --- |
| CPA(캘리포니아) | The [!DNL California Consumer Privacy Act] (CCPA) enhances privacy rights and consumer protection for residents of California, United States. CPA는 캘리포니아 거주자들에게 개인 데이터를 액세스 및 삭제할 권리, 개인 데이터가 판매되거나 공개(및 누구에게) 되었는지, 그리고 자신의 데이터를 제3자에게 판매하지 못하도록 거부할 수 있는 권리 등 새로운 데이터 개인정보 보호 권한을 제공합니다.<br/><br/>추가 문서를 위한 링크: <ul><li>[법률 개요](https://oag.ca.gov/privacy/ccpa)</li><li>[CPA FAQ](ccpa/faq.md)</li></ul> |
| GDPR(유럽 연합) | The [!DNL General Data Protection Regulation] (GDPR) introduced several new data privacy rights for members of the European Union, including the **Right to Access** and the **Right to be Forgotten**. 이것은 귀사가 개인 데이터를 수집한 모든 대상 EU 사용자는 언제든지 자신의 데이터에 대한 액세스나 삭제를 요청할 수 있음을 의미합니다. <br/><br/>추가 문서를 위한 링크: <ul><li>[법률 개요](https://gdpr-info.eu/)</li><li>[GDPR FAQ](gdpr/faq.md)</li><li>[GDPR 용어](gdpr/terminology.md)</li></ul> |
| LGPD(브라질) | LGPD [!DNL Lei Geral de Proteção de Dados] (LGPD)는 브라질의 모든 개인 또는 자연인의 개인 정보를 처리하는 것을 규제하기 위한 것이다. LGPD는 브라질 시민들에게 개인 정보를 액세스하고 삭제할 수 있는 권리, 개인 데이터가 판매 또는 공개(및 대상) 여부, 그리고 제3자에게 자신의 데이터를 판매하는 것을 거부할 수 있는 권리를 제공합니다.<br/><br/>추가 문서를 위한 링크: <ul><li>[법률 개요](https://gdpr.eu/gdpr-vs-lgpd/)</li></ul> |
| PDPA(태국) | 태국 [!DNL Personal Data Protection Act] (PDPA)는 태국 데이터 소유자들이 자신의 개인 데이터를 불법 수집, 사용 또는 공개하는 것을 방지하기 위해 도입되었습니다. 유럽 연합의 GDPR에서 영감을 얻은 이 규제는 태국 시민들에게 저장된 개인 정보에 대한 액세스 또는 삭제를 요청할 수 있는 권한을 부여하고 있습니다.<br/><br/>추가 문서를 위한 링크: <ul><li>[법률 개요](https://www.dataprotectionreport.com/2020/02/thailand-personal-data-protection-law/)</li><li>[PDPA FAQ](pdpa-tha/faq.md)</li><li>[PDPA 용어](pdpa-tha/terminology.md)</li></ul> |

데이터 작업이 위의 규정 중 어느 하나의 목적을 이루는 경우, 문서를 검토하여 고객에게 제공하는 특정 개인정보 보호 권리, 개인정보 보호 요청을 준수하기 위한 규정 준수 여부와 같은 중요한 정보를 확인하십시오. 이 정보는 CRM 시스템 [!DNL Privacy Service] 에 통합하는 방법 및 고객이 개인 정보를 요청하기 위해 웹 사이트와 상호 작용하는 방법을 결정할 때 고려해야 합니다.

법적 규정 외에 조직에 적용되는 조직 또는 산업 표준도 이러한 의사 결정을 내릴 때 고려해야 합니다.

### 개인 정보 요청에 대한 레이블 데이터 {#label}

사용 중인 [!DNL Experience Cloud] 응용 프로그램에 따라 개인 정보 요청에 응답하여 액세스하거나 삭제해야 하는 특정 데이터 필드에 레이블을 지정해야 합니다. 데이터 레이블 지정 프로세스는 애플리케이션에 따라 다릅니다. 지원되는 각 Adobe 응용 프로그램의 데이터에 레이블을 지정하는 방법에 대해 알아보려면 [Experience Cloud 응용 프로그램의 문서를 참조하십시오](./experience-cloud-apps.md).

### 전송할 ID 데이터 유형 결정 [!DNL Privacy Service] {#identity}

고객의 개인 정보 보호 요청을 [!DNL Privacy Service] 처리하려면 해당 고객에 대해 하나 이상의 고유한 ID 값을 요청 자체에서 제공해야 합니다. 고유 ID 값은 개인 및 데이터 저장소 내에 저장된 개인 데이터를 식별하는 데 사용할 수 있는 모든 [!DNL Experience Cloud] 정보입니다. [!DNL Privacy Service] 이 ID 정보를 사용하여 요청의 특성에 따라 고객의 개인 데이터를 찾아 처리합니다(액세스, 삭제 또는 수신 거부).

CRM 시스템이 사용하는 [!DNL Experience Cloud] 응용 프로그램에 따라 각 고객에 제공해야 하는 ID 값의 유형과 수는 달라집니다. 일부 응용 프로그램은 자체 내부 고객 ID 값(예: Adobe Target ID)을 사용하는 반면, 다른 솔루션은 모든 [!DNL Experience Cloud Identity Service] [!DNL Experience Cloud] 응용 프로그램에서 고객 활동을 추적하는 Adobe(ECID)의 글로벌 식별자를 사용합니다. 또한 이메일 주소 또는 전화 번호와 같은 일반 개인 정보도 유효한 ID 데이터 역할을 할 수 있습니다.

개인 정보 요청의 [ID 데이터에 대한](./identity-data.md) 문서는 허용되는 ID 정보의 유형에 대한 자세한 정보를 제공합니다 [!DNL Privacy Service]. 또한 이 문서에서는 Adobe 기술을 활용하여 고객이 웹 사이트와 상호 작용할 때 고객의 적절한 ID 정보를 효과적으로 검색하고 해당 데이터를 API 요청 [!DNL Privacy Service] 으로 전송하는 방법에 대한 지침을 제공합니다.

### 개인 정보 요청 시작 {#requests}

비즈니스 개인 정보 보호 요구 사항을 결정하고 전송할 ID 값을 결정하면 개인 정보 보호 요청 [!DNL Privacy Service]을 시작할 수 있습니다. [!DNL Privacy Service] API 또는 UI를 통해 개인 정보 요청을 전송할 수 있도록 해줍니다.

>[!IMPORTANT]
>
>아래 섹션에서는 API 또는 UI에서 일반 개인 정보 요청을 만드는 방법을 설명하는 설명서에 대한 링크를 제공합니다. 그러나 사용 중인 [!DNL Experience Cloud] 응용 프로그램에 따라 요청 페이로드에서 전송해야 하는 필드는 이러한 안내서에 표시된 예제와 다를 수 있습니다.
>
>API 또는 UI 가이드와 함께 할 때 특정 응용 프로그램에 대한 개인 정보 요청의 형식을 지정하는 방법에 대한 자세한 설명은 [Privacy Service 및 Experience Cloud 응용](./experience-cloud-apps.md) 프로그램에 대한 문서를 참조하십시오 [!DNL Experience Cloud] .
>
>또한 개인 정보 요청은 Experience Cloud 응용 프로그램에서 비동기식으로 처리됩니다. Privacy Service에서 요청을 받으면 각 애플리케이션이 요청을 완료하는 데 몇 분에서 몇 주가 걸릴 수 있습니다. 각 요청을 완료하는 데 걸리는 시간은 작업 중인 응용 프로그램에 따라 다르며 처리해야 하는 데이터의 양입니다.

#### API 사용

RESTful API 호출을 사용하여 개인 정보 작업을 만들고 관리하기 위한 여러 가지 끝점이 [[!DNL Privacy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) 제공되므로 응용 프로그램에 대한 개인 정보 보호 규정 준수에 프로그래밍 방식으로 액세스할 수 [!DNL Experience Cloud] 있습니다. API 사용 방법에 대한 자세한 내용은 [Privacy Service API 개발자 안내서를 참조하십시오](api/getting-started.md).

#### UI 사용

>[!NOTE]
>
>현재 [!DNL Privacy Service] UI는 액세스 및 삭제 요청만 지원합니다. 모든 옵트아웃 요청은 API를 통해 해야 합니다.

이 [!DNL Privacy Service] UI를 사용하면 그래픽 인터페이스를 사용하여 개인 정보 작업을 만들고 모니터링할 수 있습니다. UI에는 모든 활성 요청의 상태를 시각적으로 표시하는 **[!UICONTROL 상태 보고서]** 위젯이 포함되어 있으며, 기본 제공 **[!UICONTROL 요청 빌더를 사용하거나 JSON 파일을 업로드하여 새 요청을 만들 수]** 있습니다. UI 사용에 대한 자세한 내용은 [Privacy Service 사용 안내서를 참조하십시오](ui/overview.md).

### 개인 정보 작업 모니터링 {#monitor}

개인 정보 보호 작업을 수행한 후에는 상태 및 결과를 모니터링할 수 있는 여러 가지 옵션이 있습니다.

| 모니터링 방법 | 설명 |
| --- | --- |
| [!DNL Privacy Service] UI | 이 [!DNL Privacy Service] UI는 모든 활성 요청의 상태를 시각적으로 표시할 수 있는 모니터링 대시보드를 제공합니다. 자세한 내용은 [Privacy Service 사용 안내서를](ui/overview.md) 참조하십시오. |
| [!DNL Privacy Service] API | API에서 제공하는 조회 끝점을 사용하여 개인 정보 작업의 상태를 프로그래밍 방식으로 모니터링할 수 [!DNL Privacy Service] 있습니다. API 사용 방법에 대한 자세한 내용은 [Privacy Service 개발자 안내서를](./api/getting-started.md) 참조하십시오. |
| [!DNL Privacy Events] | [!DNL Privacy Events] 구성된 웹 후크에 전송된 Adobe I/O 이벤트를 활용하여 효율적인 작업 요청 자동화를 촉진합니다. 작업이 완료되었는지 또는 워크플로우 내의 특정 이정표에 도달했는지 확인하기 위해 [!DNL Privacy Service] API를 폴링할 필요가 없어집니다. 자세한 내용은 개인 정보 이벤트 [구독에](./privacy-events.md) 대한 자습서를 참조하십시오. |

## 다음 단계

본 문서는 서비스의 기능 사용을 시작하는 데 필요한 주요 단계 [!DNL Privacy Service] 와 간략한 개요를 제공했습니다. 다양한 작업 영역에 대한 자세한 내용은 개요 전체에 연결된 설명서를 참조하십시오 [!DNL Privacy Service].
