---
keywords: Experience Platform;홈;인기 항목;GDPR;gdpr;CCPA:PDPA;PDPA;pdpa_that;PDPA_THA;lgpd;LGPD;lgpd_bra;LGPD_BRA;
solution: Experience Platform
title: Privacy Service 개요
description: Privacy Service을 사용하면 Experience Cloud 데이터 작업에서 법적 개인 정보 보호 규정을 자동으로 준수할 수 있습니다.
exl-id: 585f7619-5072-413b-9a62-be0ea0cd4d1b
source-git-commit: 3296209a15a5f88ab14e16de25d554b9df712445
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 5%

---

# [!DNL Privacy Service] 개요

>[!IMPORTANT]
>
>Adobe Experience Platform Privacy Service에 대한 권한을 개선하여 세부기간 수준을 늘렸습니다. 이러한 변경 사항으로 조직 관리자는 원하는 역할 및 권한 수준을 사용하여 더 많은 사용자에게 액세스 권한을 부여할 수 있습니다. 이 임박한 업데이트가 기술 계정 사용자에게 중요한 변경 사항이므로 기술 계정 사용자는 Privacy Service 권한을 업데이트해야 합니다. 이 권한 변경의 적용은 **2023년 4월 13일**. 다음 문서를 참조하십시오. [레거시 API 자격 증명 마이그레이션](./permissions.md#migrate-tech-accounts) 이 문제 해결에 대한 지침은
>
>기술 계정은 엔터프라이즈 고객이 사용할 수 있으며 Adobe 개발자 콘솔을 통해 만들 수 있습니다. 기술 계정 소유자의 Adobe ID은 `@techacct.adobe.com`. 기술 계정 보유자인지 확실하지 않은 경우 조직 관리자에게 문의하십시오.

더 나은 고객 경험을 전달하려면 고객의 개인 데이터를 수집하고 저장해야 합니다. 이 데이터를 사용할 때는 고객의 개인 정보를 이해하고 존중하는 것이 중요합니다. 새로운 법률 및 조직 규정은 사용자가 요청 시 데이터 저장소에서 개인 데이터를 액세스하거나 삭제할 수 있는 권한을 제공합니다.

Adobe Experience Platform [!DNL Privacy Service] 는 고객의 개인 데이터를 관리하는 데 기업의 요구 방식이 근본적으로 변화함에 따라 개발되었습니다. 의 주요 목적 [!DNL Privacy Service] 는 위반될 경우 비즈니스에 중요한 벌금을 부과하고 데이터 작업을 중단시킬 수 있는 데이터 개인 정보 보호 규정 준수를 자동화하는 것입니다.

[!DNL Privacy Service] 는 고객 데이터 요청을 관리하는 데 도움이 되는 RESTful API 및 사용자 인터페이스를 제공합니다. 사용 [!DNL Privacy Service], Adobe Experience Cloud 애플리케이션에서 개인 고객 데이터에 액세스하고 삭제하기 위한 요청을 제출할 수 있으므로 법적 및 조직의 개인 정보 보호 규정을 자동으로 준수할 수 있습니다.

>[!IMPORTANT]
>
>Privacy Service은 데이터 주체 및 소비자 권한 요청에 대해서만 사용됩니다. 데이터 정리 또는 유지 관리에 대한 다른 Privacy Service 사용은 지원되거나 허용되지 않습니다. Adobe은 적시에 그것들을 이행할 법적 의무가 있다. 따라서 Privacy Service에 대한 로드 테스트는 프로덕션 전용 환경이며, 유효한 개인 정보 보호 요청의 불필요한 백로그를 사용하므로 허용되지 않습니다.
>
>서비스 남용을 방지하기 위해 이제 하루 동안 하드 업로드 제한이 적용됩니다. 이 시스템을 악용한 사용자는 이 서비스에 대한 액세스 권한을 잃게 됩니다. 그런 다음 해당 Privacy Service과 함께 자신의 행동에 대해 논의하고 허용 가능한 사용 방법에 대해 논의할 예정입니다.

## 시작하기 [!DNL Privacy Service] {#getting-started}

를 사용하려면 [!DNL Privacy Service], 조직의 개인 정보 보호 요구 사항, 고객으로부터 수집하는 id 데이터의 종류, 서비스와 CRM 시스템을 연결하는 가장 좋은 방법 등 몇 가지 주요 사항을 결정해야 합니다.

이러한 결정은 다음 질문을 통해 요약할 수 있습니다.

1. **고객으로부터 어떤 정보를 수집하고 있습니까?**
   * 다음을 최대한 활용하려면 [!DNL Privacy Service], 고객으로부터 수집하는 데이터의 유형과 이러한 데이터 유형에 대한 개인 정보 보호 규정을 준수해야 합니다. 의 섹션을 참조하십시오. [개인 정보 보호 요구 사항 확인](#requirements) 추가 정보.
1. **데이터에 올바르게 레이블을 지정했습니까?**
   * 서비스에서 개인 정보 작업 중에 액세스하거나 삭제할 필드를 결정하려면 데이터에 레이블이 제대로 지정되어야 합니다. 의 섹션을 참조하십시오. [레이블 지정 데이터](#label) 추가 정보.
1. **보낼 ID를 알고 있습니까? [!DNL Privacy Service]?**
   * 개인 정보 보호 요청을 보낼 때 특정 Adobe 애플리케이션별 개별 고객 ID를 제공해야 합니다. 의 섹션을 참조하십시오. [id 데이터 제공](#identity)  및 [개인 정보 보호 요청 만들기](#requests) 추가 정보.
1. **개인 정보 보호 작업을 어떻게 추적합니까?**
   * 개인 정보 요청을 수행하면 해당 상태 및 결과를 추적하는 몇 가지 옵션이 있습니다. 의 섹션을 참조하십시오. [개인 정보 작업 모니터링](#monitor) 추가 정보.

아래 섹션에서는 이러한 중요한 전제 조건 단계에 대한 일반적인 지침을 제공하고 추가 페이지에 대한 링크를 제공합니다 [!DNL Privacy Service] 자세한 내용은 설명서 를 참조하십시오.

### 조직의 개인 정보 보호 요구 사항 확인 {#requirements}

비즈니스의 성격과 운영되는 관할 구역에 따라 데이터 운영에 법적 개인 정보 보호 규정이 적용될 수 있습니다. 이러한 규정에서는 고객에게 수집된 데이터에 대한 액세스를 요청할 수 있는 권한과 저장된 데이터의 삭제를 요청할 수 있는 권한을 부여하는 경우가 많습니다. 개인 데이터에 대한 이러한 고객 요청을 설명서 전체에서 &quot;개인 정보 보호 요청&quot;이라고 합니다.

다음과 같은 다양한 법적 개인 정보 보호 규정에 대한 자세한 내용 [!DNL Privacy Service] 는 주요 용어와 자주 묻는 질문에 대한 답변을 포함하여 요청을 관리합니다. [개인 정보 보호 규정 문서](./regulations/overview.md).

데이터 작업이 지원되는 규정의 목적에 속하는 경우 고객에게 제공되는 특정 개인 정보 보호 권한 및 개인 정보 보호 요청을 이행하기 위한 규정 준수 창과 같은 중요한 정보에 대해 설명서를 검토하십시오. 이 정보는 통합 방법을 결정할 때 고려해야 합니다 [!DNL Privacy Service] 개인 정보 보호 요청을 수행하기 위해 고객이 웹 사이트와 상호 작용하는 방법 을 CRM 시스템에 추가하는 방법을 설명합니다.

법적 규정 외에 조직에 적용되는 조직 또는 업계 표준도 이러한 결정을 내릴 때 고려해야 합니다.

### 개인 정보 요청에 대한 데이터에 레이블 지정 {#label}

에 따라 [!DNL Experience Cloud] 사용 중인 응용 프로그램은 개인 정보 보호 요청에 응답하여 액세스하거나 삭제해야 하는 특정 데이터 필드에 레이블을 지정해야 합니다. 데이터에 레이블을 지정하는 프로세스는 애플리케이션마다 다릅니다. 지원되는 각 Adobe 응용 프로그램의 데이터에 레이블을 지정하는 방법에 대해 알아보려면 다음 문서를 참조하십시오 [Experience Cloud 애플리케이션](./experience-cloud-apps.md).

### 보낼 ID 데이터 유형 결정 [!DNL Privacy Service] {#identity}

대상 [!DNL Privacy Service] 고객의 개인 정보 보호 요청을 처리하려면 해당 고객에 대한 하나 이상의 고유 ID 값을 요청 자체에 제공해야 합니다. 고유한 ID 값은 개인 및 저장된 개인 데이터를 식별하는 데 사용할 수 있는 모든 정보입니다 [!DNL Experience Cloud] 데이터 저장소. [!DNL Privacy Service] 이 id 정보를 사용하여 요청의 특성(액세스, 삭제 또는 옵트아웃)에 따라 고객의 개인 데이터를 찾아 처리합니다.

에 따라 [!DNL Experience Cloud] crm 시스템이 사용하는 응용 프로그램, 각 고객에 대해 제공해야 하는 ID 값의 유형 및 수는 달라집니다. 일부 애플리케이션은 자체 내부 고객 ID 값(예: Adobe Target ID)을 활용하는 반면, 다른 솔루션은 Adobe의 글로벌 식별자를 사용합니다 [!DNL Experience Cloud Identity Service] 모든 위치에서 고객 활동을 추적하는 ECID [!DNL Experience Cloud] 응용 프로그램. 또한 이메일 주소나 전화번호와 같은 일반적인 개인 정보도 유효한 ID 데이터로 사용할 수 있습니다.

문서 [개인 정보 보호 요청에 대한 id 데이터](./identity-data.md) 에 허용되는 id 정보 유형에 대한 자세한 정보를 제공합니다. [!DNL Privacy Service]. 또한 Adobe 기술을 활용하여 고객이 웹 사이트와 상호 작용할 때 고객으로부터 적절한 ID 정보를 효과적으로 검색하고 해당 데이터를 로 전송하는 방법에 대한 지침을 제공합니다 [!DNL Privacy Service] 를 반환합니다.

### 개인 정보 보호 요청 만들기 시작 {#requests}

기업의 개인 정보 보호 요구 사항을 결정하고 전송할 ID 값을 결정하면 [!DNL Privacy Service], 개인 정보 보호 요청 만들기를 시작할 수 있습니다. [!DNL Privacy Service] api 또는 UI를 통해 개인 정보 요청을 보낼 수 있습니다.

>[!IMPORTANT]
>
>아래 섹션에서는 API 또는 UI에서 일반 개인 정보 보호 요청을 수행하는 방법을 다루는 설명서에 대한 링크를 제공합니다. 그러나, [!DNL Experience Cloud] 사용 중인 응용 프로그램에서 요청 페이로드에서 보내야 하는 필드는 이 안내서에 표시된 예와 다를 수 있습니다.
>
>API 또는 UI 안내서를 따라 다음 문서를 참조하십시오. [Privacy Service 및 Experience Cloud 애플리케이션](./experience-cloud-apps.md) 특정 사용자에 대한 개인 정보 보호 요청의 형식을 지정하는 방법에 대한 추가 설명서입니다 [!DNL Experience Cloud] 애플리케이션
>
>개인 정보 보호 요청은 Experience Cloud 애플리케이션 간에 비동기적으로 처리됩니다. Privacy Service이 요청을 받으면 각 애플리케이션이 요청을 완료하는 데 몇 분에서 몇 주 정도 걸릴 수 있습니다. 각 요청을 완료하는 데 걸리는 시간은 작업 중인 응용 프로그램과 처리해야 하는 데이터 양에 따라 다릅니다.

#### API 사용

다음 [[!DNL Privacy Service API]](https://www.adobe.io/experience-platform-apis/references/privacy-service/) 에서는 RESTful API 호출을 사용하여 개인 정보 작업을 만들고 관리하기 위한 여러 엔드포인트를 제공하므로, 사용자 지정 규칙에 대해 프로그래밍 방식으로 접근 할 수 있습니다 [!DNL Experience Cloud] 응용 프로그램. API 사용 방법에 대한 자세한 단계는 [Privacy Service API 안내서](api/overview.md).

#### UI 사용

>[!NOTE]
>
>다음 [!DNL Privacy Service] UI는 현재 액세스 및 삭제 요청만 지원합니다. 모든 옵트아웃 요청은 API를 통해 대신 해야 합니다.

다음 [!DNL Privacy Service] UI를 사용하면 그래픽 인터페이스를 사용하여 개인 정보 작업을 만들고 모니터링할 수 있습니다. UI에는 **[!UICONTROL 상태 보고서]** 모든 활성 요청의 상태를 시각적으로 표시하고 기본 제공 요청을 사용하여 새 요청을 만들 수 있도록 해주는 위젯입니다 **[!UICONTROL 요청 빌더]** 또는 JSON 파일을 업로드하여 검색할 수 있습니다. UI 사용에 대한 자세한 내용은 [Privacy Service 사용 안내서](ui/overview.md).

### 개인 정보 작업 모니터링 {#monitor}

개인 정보 보호 작업을 수행하면 해당 상태 및 결과를 모니터링할 수 있는 다음과 같은 몇 가지 옵션이 있습니다.

| 모니터링 방법 | 설명 |
| --- | --- |
| [!DNL Privacy Service] UI | 다음 [!DNL Privacy Service] UI는 모든 활성 요청의 상태를 시각적으로 나타낼 수 있도록 해주는 모니터링 대시보드를 제공합니다. 자세한 내용은 [Privacy Service 사용 안내서](ui/overview.md) 추가 정보. |
| [!DNL Privacy Service] API | 에서 제공하는 조회 끝점을 사용하여 개인 정보 작업의 상태를 프로그래밍 방식으로 모니터링할 수 있습니다 [!DNL Privacy Service] API. 자세한 내용은 [Privacy Service API 안내서](./api/overview.md) 를 참조하십시오. |
| [!DNL Privacy Events] | [!DNL Privacy Events] 구성된 웹 후크에 전송된 Adobe I/O 이벤트를 활용하여 효율적인 작업 요청 자동화를 수행할 수 있습니다. 그들은 그 조사를 할 필요성을 줄이거나 없앤다 [!DNL Privacy Service] 작업이 완료되었는지 또는 워크플로우 내의 특정 이정표에 도달했는지 확인하기 위한 API입니다. 다음에서 자습서를 참조하십시오. [개인 정보 보호 이벤트 가입](./privacy-events.md) 추가 정보. |

## 다음 단계

이 문서에서는 [!DNL Privacy Service] 서비스 기능을 사용하기 시작하는 데 필요한 주요 단계입니다. 작업 시 다양한 측면에 대한 자세한 내용은 개요 전체에서 에 연결된 설명서를 참조하십시오 [!DNL Privacy Service].
