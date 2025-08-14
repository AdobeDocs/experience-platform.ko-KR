---
title: Experience Platform 프리릴리스 노트
description: Adobe Experience Platform의 최신 릴리스 정보 미리보기.
hide: true
hidefromtoc: true
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: bcf3045fbbf4f9673e954a5ebf95d1225d4cdcd7
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 35%

---

# Adobe Experience Platform 프리릴리스 노트

>[!IMPORTANT]
>
>이 문서는 이번 달 릴리스 정보의 **미리 보기**&#x200B;로 작성되었습니다. 릴리스 항목은 변경될 수 있으며 최종 릴리스에서 추가 또는 제거될 수 있습니다.

>[!TIP]
>
>다른 Adobe Experience Platform 애플리케이션의 릴리스 정보는 다음 문서를 참조하십시오.
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/ko/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/releases/pre-release-notes)
>- [페더레이션된 대상자 컴포지션](https://experienceleague.adobe.com/ko/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/ko/docs/real-time-cdp-collaboration/using/latest)

**릴리스 날짜: 2025년 8월**

Adobe Experience Platform의 새로운 기능 및 기존 기능 업데이트:

- [경고](#alerts)
- [대상](#destinations)
- [경험 데이터 모델 (XDM)](#xdm)
- [Segmentation Service](#segmentation-service)
- [소스](#sources)

## 경고 {#alerts}

Experience Platform을 통해 다양한 Experience Platform 활동에 대한 이벤트 기반 알림을 구독할 수 있습니다. Experience Platform 사용자 인터페이스의 [!UICONTROL 경고] 탭을 통해 다양한 경고 규칙을 구독할 수 있으며, 원하는 경우 UI 자체 또는 이메일 알림을 통해 알림 메시지를 수신할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 스트리밍 처리량 용량 경고 | 세 가지 새로운 경고를 통해 사용자는 경고를 구독하고 구성하여 스트리밍 처리량 용량의 성능을 사전 예방적으로 관리 및 모니터링할 수 있습니다. 새로운 경고에는 스트리밍 처리량이 80%, 90%에 도달하거나 용량 제한을 초과하는 경우가 포함됩니다. 자세한 내용은 [용량 경고 규칙](../observability/alerts/rules.md#capacity) 안내서를 참조하십시오. |

경고에 대한 자세한 내용은 [[!DNL Observability Insights] 개요](../observability/home.md)를 참조하십시오.

## 대상 {#destinations}

[!DNL Destinations]은(는) Experience Platform의 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 빌드된 통합입니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타기팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

>[!IMPORTANT]
>
>**데이터 집합 내보내기 일정 확장**
>
>조직에 2024년 11월 이전에 만들어진 데이터 세트 내보내기 데이터 흐름이 있는 경우 이러한 데이터 흐름은 **2025년 9월 1일**&#x200B;에 작동을 중지합니다. 2025년 9월 1일 이후에도 데이터 흐름을 계속 내보내려면 [이 안내서](../destinations/ui/dataset-expiration-update.md)의 단계를 따라 데이터 세트를 내보내는 각 대상에 대한 일정을 확장해야 합니다.

**새로운 대상**

| 대상 | 설명 |
| --- | --- |
| [!DNL Acxiom Real ID Audience] 대상 | [!DNL Acxiom Real ID Audience Connection] 대상을 사용하여 [!DNL Acxiom's] [Real ID™](https://www.acxiom.com/real-id/real-id/) 기술로 대상을 향상하고 [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] 등과 같은 여러 플랫폼으로 대상을 활성화하십시오. |

**업데이트된 대상**

| 대상 | 설명 |
| --- | --- |
| [!DNL LinkedIn] 및 [!DNL Pinterest] 대상에 대한 인증 만료 세부 정보 | 이제 계정 만료 정보가 Experience Platform 인터페이스에 바로 표시되므로 [!DNL LinkedIn] 및 [!DNL Pinterest] 인증이 만료되고 갱신되어 데이터 흐름이 중단되기 전에 이를 확인할 수 있습니다. |
| [!DNL Data Landing Zone] 대상에 대한 암호화 지원 | 암호화를 사용하여 내보낸 데이터를 보호합니다. 이제 RSA 형식의 공개 키를 연결하여 내보낸 파일을 암호화할 수 있으므로 다른 클라우드 스토리지 대상이 중요한 정보를 제공하는 것과 동일한 수준의 보안을 제공합니다. |
| [[!DNL Microsoft Bing]](../destinations/catalog/advertising/bing.md) 내부 업그레이드 | 2025년 8월 11일 화요일부터 대상 카탈로그에 두 개의 **[!DNL Microsoft Bing]** 카드가 나란히 표시됩니다. 이는 대상 서비스의 내부 업그레이드로 인한 변경 사항입니다. 기존 **[!DNL Microsoft Bing]** 대상 커넥터의 이름이 **[!UICONTROL (더 이상 사용되지 않음) Microsoft Bing]**(으)로 변경되었으며 이제 이름이 **[!UICONTROL Microsoft Bing]**&#x200B;인 새 카드를 사용할 수 있습니다. 새 활성화 데이터 흐름에 대해 카탈로그의 새 **[!UICONTROL Microsoft Bing]** 연결을 사용하십시오. **[!UICONTROL (더 이상 사용되지 않는) Microsoft Bing]** 대상에 대한 활성 데이터 흐름이 있는 경우 자동으로 업데이트되므로 사용자의 작업이 필요하지 않습니다. <br><br> [Flow Service API](https://developer.adobe.com/experience-platform-apis/references/destinations/)를 통해 데이터 흐름을 생성하는 경우 [!DNL flow spec ID] 및 [!DNL connection spec ID]를 다음 값으로 업데이트해야 합니다.<ul><li>흐름 사양 ID: `8d42c81d-9ba7-4534-9bf6-cf7c64fbd12e`</li><li>연결 사양 ID: `dd69fc59-3bc5-451e-8ec2-1e74a670afd4`</li></ul> 이 업그레이드 후에는 **데이터 흐름에서**&#x200B;활성화된 프로필 수[!DNL Microsoft Bing]이(가) 감소할 수 있습니다. 이 삭제는 이 대상 플랫폼에 대한 모든 활성화에 대한 **ECID 매핑 요구 사항**&#x200B;의 도입으로 인해 발생합니다. |
| 대상 카드 통합 [!DNL Marketo]개 | 통합 대상 카드를 사용하여 [!DNL Marketo] 대상 설정을 단순화합니다. [!DNL Marketo]개의 V2 및 V3 카드를 하나의 간소화된 옵션으로 통합했기 때문에 올바른 대상을 쉽게 선택하고 빠르게 시작할 수 있습니다. |

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 대상에 대한 검색, 필터링 및 태그 지정 기능 향상 | 찾아보기 및 계정 탭에서 향상된 검색, 필터링 및 태그 지정 기능을 통해 대상 관리 워크플로를 개선합니다. 이제 이름별로 특정 데이터 흐름 및 계정을 검색하고, 대상 플랫폼, 상태 및 날짜를 포함한 다양한 기준으로 필터링하고, 사용자 지정 태그를 만들어 대상을 구성할 수 있습니다. 마지막 데이터 흐름 실행 시간과 같은 주요 필드에도 열 정렬을 사용할 수 있으므로 대상 연결을 보다 쉽게 식별하고 관리할 수 있습니다. |

자세한 내용은 [대상 개요](../destinations/home.md)를 참조하십시오.

## 경험 데이터 모델 (XDM) {#xdm}

XDM은 Experience Platform으로 가져온 데이터에 대한 일반적인 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수하여 모든 고객 경험 데이터를 공통된 표현에 통합해 보다 빠르고 통합된 방식으로 인사이트를 제공할 수 있습니다. 고객 조치에서 귀중한 인사이트를 얻고, 세그먼트를 통해 고객 대상자를 정의하고, 개인 설정 목적으로 고객 속성을 사용할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 모델 기반 스키마 | 모델 기반 스키마를 사용하여 데이터 모델링을 단순화합니다. 이제 포괄적인 사용 방법 예제와 지침을 통해 스키마를 보다 쉽게 만들 수 있습니다. 이 기능은 현재 Campaign Orchestration 라이선스 소유자가 사용할 수 있으며 GA 시점에 데이터 Distiller 고객으로 확장되어 데이터 모델링에 더 쉽게 액세스하고 효율적으로 작업할 수 있습니다. |

자세한 내용은 [XDM 개요](../xdm/home.md)를 참조하십시오.

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service]는 고객 기반 내에서 마케팅 가능한 사용자 그룹을 구분하는 기준을 설명하여 프로필의 특정 하위 집합을 정의합니다. 대상자는 기록 데이터(예: 인구 통계 정보) 또는 고객과 브랜드의 상호 작용을 나타내는 시계열 이벤트를 기반으로 할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 대상자 예상 | 이제 대상자 예상 값이 세그먼트 빌더 내에서 자동으로 생성됩니다. 이 값은 대상자를 수정할 때마다 업데이트되며 항상 최신 대상자 규칙을 반영합니다. |

자세한 내용은 [[!DNL Segmentation Service] 개요](../segmentation/home.md)를 참조하십시오.

## 소스 {#sources}

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| UI에서 [!BADGE Beta]{type=Informative} Azure 개인 링크 지원 | 개인 네트워크 연결을 통해 데이터를 안전하게 보호합니다. 이제 개인 끝점을 만들고 공용 인터넷을 우회하는 데이터 흐름을 설정하여 중요한 데이터에 대한 보안 및 네트워크 격리를 강화할 수 있습니다. |
| [!DNL Marketo] 소스 설명서 업데이트 | Experience Platform에 들어갈 때 [!DNL Marketo] 데이터가 변환되는 방식을 완벽하게 파악할 수 있습니다. 이제 모든 필드 매핑에 데이터 변환에 대한 자세한 설명이 포함되어 있으므로 `PersonID`이(가) `leadID`이(가) 되고 `eventType`이(가) `activityType`이(가) 되는 방식을 정확하게 이해할 수 있습니다. |
| [!DNL Azure Blob Storage]에 대한 서비스 사용자 인증 지원 | 이제 서비스 사용자 인증을 사용하여 [!DNL Azure Blob Storage] 계정을 Experience Platform에 연결할 수 있습니다. |

자세한 내용은 [소스 개요](../sources/home.md)를 참조하십시오.

<!--

## Query Service {#query-service}

Adobe Experience Platform Query Service provides a robust SQL interface for data analysis and exploration across the platform.

**New or updated features**

| Feature | Description |
| ------- | ----------- |
| Data Distiller Session Management | Take control of your data analysis sessions with enhanced session management. You can now monitor and manage your sessions more effectively across development and production environments, giving you better visibility into your query performance and resource usage. |

For more information, read the [Query Service overview](../query-service/home.md).

## B2B CDP {#b2b-cdp}

Real-Time CDP B2B Edition provides comprehensive B2B customer data management capabilities, enabling organizations to build unified customer profiles, create sophisticated B2B audiences, and activate data across various marketing channels.

**New or updated features**

| Feature | Description |
| ------- | ----------- |
| Lookup Support for B2B Classes Only | Streamline your B2B data access with focused lookup support. You can now look up Person (Profile), Experience Events, Account, and Opportunity entities directly through the Entities API. This simplified approach helps you access the most important B2B data more efficiently while reducing complexity. |
| B2B Namespace and Schema Updates | Experience a cleaner, more streamlined B2B data model. We've simplified the B2B namespace and schema structure by removing complex relationship mappings and non-primary identity support for certain B2B classes. This makes your B2B data easier to work with and understand. |

For more information, read the [Real-Time CDP B2B Edition overview](../rtcdp/b2b-overview.md).

-->
