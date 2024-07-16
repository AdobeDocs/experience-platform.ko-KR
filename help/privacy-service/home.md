---
keywords: Experience Platform;홈;인기 항목;GDPR;gdpr;ccpa:CCPA;PDPA;PDPA;pdpa_that;PDPA_THA;lgpd;LGPD;lgpd_bra;LGPD_BRA;
solution: Experience Platform
title: Privacy Service 개요
description: Privacy Service을 통해 Experience Cloud 데이터 운영에서 법적 개인정보 보호 규정을 자동으로 준수하는 방법에 대해 알아봅니다.
exl-id: 585f7619-5072-413b-9a62-be0ea0cd4d1b
source-git-commit: 19b33ddf2fc3f8d889d370eedfc732ac54178dcd
workflow-type: tm+mt
source-wordcount: '1532'
ht-degree: 5%

---

# Privacy Service 개요

더 나은 고객 경험을 게재하려면 고객의 개인 데이터를 수집하고 저장해야 합니다. 이 데이터를 사용할 때는 고객의 개인 정보를 이해하고 존중하는 것이 중요합니다. 새로운 법률 및 조직 규정은 사용자가 요청 시 데이터 저장소에서 개인 데이터를 액세스하거나 삭제할 수 있는 권한을 제공합니다.

Adobe Experience Platform Privacy Service은 비즈니스가 고객의 개인 데이터를 관리하는 데 필요한 방식의 근본적인 변화에 따라 개발되었습니다. Privacy Service의 핵심 목적은 데이터 개인 정보 보호 규정 준수를 자동화하는 것입니다. 이를 위반할 경우 큰 벌금이 부과되고 비즈니스의 데이터 운영에 차질을 빚을 수 있습니다.

Privacy Service은 고객 데이터 요청을 관리하는 데 도움이 되는 RESTful API 및 사용자 인터페이스를 제공합니다. Privacy Service을 사용하여 Adobe Experience Cloud 애플리케이션에서 개인 고객 데이터에 액세스하고 삭제하는 요청을 제출할 수 있으므로 법적 및 조직의 개인 정보 보호 규정을 자동으로 준수할 수 있습니다.

>[!IMPORTANT]
>
>Privacy Service은 데이터 주체 및 소비자 권한 요청용으로만 사용됩니다. 데이터 정리 또는 유지 관리를 위한 다른 Privacy Service 사용은 지원되지 않거나 허용되지 않습니다. Adobe은 적시에 이를 이행할 법적 의무가 있다. 따라서 프로덕션 전용 환경이며 유효한 개인 정보 보호 요청에 대한 불필요한 백로그를 만들기 때문에 Privacy Service에 대한 로드 테스트는 허용되지 않습니다.
>
>이제 서비스 남용을 방지하기 위해 엄격한 일일 업로드 제한이 적용됩니다. 시스템을 남용하는 것으로 확인된 사용자는 서비스에 액세스할 수 없게 됩니다. 그런 다음 후속 회의가 그들과 함께 개최되어 그들의 행동에 대해 이야기하고 Privacy Service에 허용되는 사용에 대해 논의합니다.

## Privacy Service 시작 {#getting-started}

Privacy Service을 최적으로 사용하려면 조직의 개인 정보 보호 요구 사항, 고객으로부터 수집하는 ID 데이터의 종류 및 CRM 시스템과 서비스를 연결하는 최상의 방법 측면에서 몇 가지 주요 결정을 내려야 합니다.

이러한 결정은 다음과 같은 질문을 통해 요약할 수 있습니다.

1. **고객으로부터 어떤 정보를 수집하고 있습니까?**
   * Privacy Service을 최대한 활용하려면 고객으로부터 수집하는 데이터의 유형과 개인정보 보호 규정의 적용 대상을 자세히 이해해야 합니다. 자세한 내용은 [개인 정보 보호 요구 사항 확인](#requirements) 섹션을 참조하십시오.
1. **데이터 레이블을 올바르게 지정했습니까?**
   * 개인 정보 보호 작업 중에 액세스하거나 삭제할 필드를 결정하려면 서비스에 대한 데이터에 올바른 레이블을 지정해야 합니다. 자세한 내용은 [데이터 레이블 지정](#label) 섹션을 참조하십시오.
1. **Privacy Service에 보낼 ID를 알고 있습니까?**
   * 개인 정보 보호 요청을 보낼 때 특정 Adobe 애플리케이션과 관련된 개별 고객 ID를 제공해야 합니다. 자세한 내용은 [ID 데이터 제공](#identity) 및 [개인 정보 보호 요청 만들기](#requests)의 섹션을 참조하십시오.
1. **개인 정보 작업을 어떻게 추적합니까?**
   * 개인 정보 보호 요청을 수행하면 상태 및 결과를 추적하는 몇 가지 옵션이 있습니다. 자세한 내용은 [개인 정보 작업 모니터링](#monitor) 섹션을 참조하십시오.

아래 섹션에서는 이러한 중요한 전제 조건 단계에 대한 일반적인 지침을 제공하며 자세한 내용은 추가 Privacy Service 설명서에 대한 링크를 제공합니다.

### 조직의 개인 정보 보호 요구 사항 결정 {#requirements}

비즈니스의 성격과 운영되는 관할 구역에 따라 데이터 운영에 법적 개인 정보 보호 규정이 적용될 수 있습니다. 이러한 규정에서는 고객에게 수집된 데이터에 대한 액세스를 요청할 수 있는 권한과 저장된 데이터의 삭제를 요청할 수 있는 권한을 부여하는 경우가 많습니다. 설명서 전체에서 개인 데이터에 대한 이러한 고객 요청을 &quot;개인 정보 보호 요청&quot;이라고 합니다.

Privacy Service에서 FAQ에 대한 주요 용어 및 답변을 포함하여 요청을 관리하는 다양한 법적 개인 정보 보호 규정에 대한 자세한 내용은 [개인 정보 보호 규정 문서](./regulations/overview.md)를 참조하십시오.

데이터 작업이 지원되는 규정의 목적에 해당하는 경우 해당 설명서를 검토하여 고객에게 제공되는 특정 개인 정보 보호 권한 및 개인 정보 보호 요청을 준수하기 위한 규정 준수 창과 같은 중요한 정보를 확인하십시오. 이 정보는 CRM 시스템에 Privacy Service을 통합하는 방법과 고객이 개인 정보 요청을 위해 웹 사이트와 상호 작용하는 방법을 결정할 때 고려되어야 합니다.

이러한 결정을 내릴 때는 법적 규정 외에도 조직에 적용되는 조직 또는 업계 표준도 고려해야 합니다.

### 개인 정보 보호 요청에 대한 레이블 데이터 {#label}

사용 중인 [!DNL Experience Cloud] 응용 프로그램에 따라 개인 정보 보호 요청에 대한 응답으로 액세스하거나 삭제해야 하는 특정 데이터 필드에 레이블을 지정해야 합니다. 데이터에 레이블을 지정하는 프로세스는 애플리케이션마다 다릅니다. 지원되는 각 Adobe 응용 프로그램의 데이터에 레이블을 지정하는 방법을 알아보려면 [Experience Cloud 응용 프로그램](./experience-cloud-apps.md)에 대한 문서를 참조하십시오.

### Privacy Service에 보낼 ID 데이터 유형 확인 {#identity}

Privacy Service이 고객의 개인 정보 보호 요청을 처리하려면 요청 자체에 해당 고객에 대한 하나 이상의 고유 ID 값을 제공해야 합니다. 고유 ID 값은 [!DNL Experience Cloud] 데이터 저장소 내에서 개별 개인 및 저장된 개인 데이터를 식별하는 데 사용할 수 있는 모든 정보입니다. Privacy Service은 이 ID 정보를 사용하여 요청의 특성(액세스, 삭제 또는 옵트아웃)에 따라 고객의 개인 데이터를 찾고 처리합니다.

CRM 시스템에서 사용하는 [!DNL Experience Cloud] 응용 프로그램에 따라 각 고객에 대해 제공해야 하는 ID 값의 유형 및 개수가 달라집니다. 일부 응용 프로그램에서는 자체 내부 고객 ID 값(예: Adobe Target ID)을 사용하는 반면, 다른 솔루션에서는 모든 [!DNL Experience Cloud] 응용 프로그램에서 고객 활동을 추적하는 ECID(Adobe [!DNL Experience Cloud Identity Service])의 전역 식별자를 사용합니다. 또한 이메일 주소나 전화번호와 같은 일반적인 개인 정보도 유효한 신원 데이터로 기능할 수 있습니다.

Privacy Service에 허용되는 ID 정보 유형에 대한 자세한 내용은 [개인 정보 보호 요청에 대한 ID 데이터](./identity-data.md)에 대한 문서를 참조하십시오. 또한 이 문서에서는 고객이 웹 사이트와 상호 작용할 때 고객으로부터 적절한 ID 정보를 효과적으로 검색하고 해당 데이터를 API 요청의 Privacy Service으로 전송하기 위해 Adobe 기술을 적용하는 방법에 대한 지침을 제공합니다.

### 개인 정보 보호 요청 시작 {#requests}

비즈니스의 개인 정보 보호 요구 사항을 결정하고 Privacy Service에 전송할 ID 값을 결정했으면 개인 정보 보호 요청을 시작할 수 있습니다. Privacy Service을 사용하여 API 또는 UI를 통해 개인 정보 요청을 전송합니다.

>[!IMPORTANT]
>
>아래 섹션에서는 API 또는 UI에서 일반적인 개인 정보 요청을 하는 방법을 다루는 설명서에 대한 링크를 제공합니다. 그러나 사용 중인 [!DNL Experience Cloud] 응용 프로그램에 따라 요청 페이로드에서 보내야 하는 필드가 이 안내서에 표시된 예와 다를 수 있습니다.
>
>API 또는 UI 안내서와 함께 따라가면서 특정 [!DNL Experience Cloud] 애플리케이션에 대한 개인 정보 보호 요청을 포맷하는 방법에 대한 자세한 내용은 [Privacy Service 및 Experience Cloud 애플리케이션](./experience-cloud-apps.md)에 대한 문서를 참조하십시오.
>
>개인 정보 보호 요청은 Experience Cloud 애플리케이션 간에 비동기적으로 처리됩니다. Privacy Service이 요청을 수신하면 각 애플리케이션이 요청을 완료하는 데 몇 분에서 몇 주 정도 걸릴 수 있습니다. 각 요청을 완료하는 데 걸리는 시간은 작업 중인 애플리케이션과 처리해야 하는 데이터의 양에 따라 다릅니다.

#### API 사용 {#api}

[!DNL Experience Cloud] 응용 프로그램에 대한 개인 정보 보호 규정 준수에 프로그래밍 방식으로 접근하려면 [[!DNL Privacy Service API]](https://developer.adobe.com/experience-platform-apis/references/privacy-service/) 끝점에 대한 RESTful API 호출을 사용하여 개인 정보 보호 작업을 만들고 관리할 수 있습니다. API 사용 방법에 대한 자세한 단계는 [Privacy Service API 안내서](api/overview.md)를 참조하십시오.

#### UI 사용 {#ui}

>[!NOTE]
>
>Privacy Service UI는 현재 액세스 및 삭제 요청만 지원합니다. 모든 옵트아웃 요청은 대신 API를 통해 수행해야 합니다.

Privacy Service UI가 있는 그래픽 인터페이스를 사용하여 개인 정보 작업을 만들고 모니터링할 수 있습니다. UI에는 모든 활성 요청의 상태를 시각적으로 표시하는 **[!UICONTROL 상태 보고서]** 위젯이 포함되어 있으며 기본 제공 **[!UICONTROL 요청 빌더]**&#x200B;를 사용하거나 JSON 파일을 업로드하여 요청을 만들 수 있습니다. UI 사용에 대한 자세한 내용은 [Privacy Service 사용 안내서](ui/overview.md)를 참조하십시오.

### 개인 정보 작업 모니터링 {#monitor}

개인 정보 작업을 완료하면 상태 및 결과를 모니터링하기 위한 몇 가지 옵션이 제공됩니다.

| 모니터링 방법 | 설명 |
| --- | --- |
| PRIVACY SERVICE UI | Privacy Service UI 모니터링 대시보드를 사용하여 모든 활성 요청의 상태를 시각적으로 볼 수 있습니다. 자세한 내용은 [Privacy Service 사용 안내서](ui/overview.md)를 참조하세요. |
| PRIVACY SERVICE API | Privacy Service API에서 제공하는 조회 끝점을 사용하여 개인 정보 작업 상태를 프로그래밍 방식으로 모니터링할 수 있습니다. API 사용 방법에 대한 자세한 단계는 [Privacy Service API 안내서](./api/overview.md)를 참조하십시오. |
| [!DNL Privacy Events] | [!DNL Privacy Events]은(는) 구성된 웹후크로 전송되는 Adobe I/O 이벤트를 사용하여 효율적인 작업 요청 자동화를 용이하게 합니다. Privacy Service API를 폴링하여 작업이 완료되었는지 또는 워크플로우 내의 특정 이정표에 도달했는지 확인할 필요가 줄어들거나 없어집니다. 자세한 내용은 [개인 정보 보호 이벤트 구독](./privacy-events.md)에 대한 자습서를 참조하십시오. |

## 다음 단계

이 문서에서는 Privacy Service에 대한 높은 수준의 개요와 서비스 기능을 사용하는 데 필요한 주요 단계를 제공했습니다. Privacy Service 작업의 다양한 측면에 대한 자세한 내용은 개요 전체에 연결된 설명서를 참조하십시오.
