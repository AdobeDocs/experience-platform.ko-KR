---
title: Adobe Experience Platform 릴리스 정보 2025년 8월
description: Adobe Experience Platform의 2025년 8월 릴리스 정보입니다.
exl-id: d93e98f3-d165-4710-ad1d-2ad3857cd0f8
source-git-commit: ba16b870b49ccd13cf927b9460e81976d8be0048
workflow-type: tm+mt
source-wordcount: '1474'
ht-degree: 88%

---

# Adobe Experience Platform 릴리스 정보

>[!TIP]
>
>다른 Adobe Experience Platform 애플리케이션의 릴리스 정보는 다음 문서를 참조하십시오.
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/ko/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/releases/pre-release-notes)
>- [페더레이션된 대상자 컴포지션](https://experienceleague.adobe.com/ko/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/ko/docs/real-time-cdp-collaboration/using/latest)

**릴리스 일자: 2025년 8월 19일**


Adobe Experience Platform의 새로운 기능 및 기존 기능 업데이트:

- [경고](#alerts)
- [카탈로그 서비스](#catalog-service)
- [대상](#destinations)
- [경험 데이터 모델 (XDM)](#xdm)
- [샌드박스](#sandboxes)
- [Segmentation Service](#segmentation-service)
- [소스](#sources)

## 경고 {#alerts}

Experience Platform을 통해 다양한 Experience Platform 활동에 대한 이벤트 기반 알림을 구독할 수 있습니다. Experience Platform 사용자 인터페이스의 [!UICONTROL Alerts] 탭을 통해 다양한 경고 규칙을 구독할 수 있으며 UI 자체 내에서 또는 이메일 알림을 통해 경고 메시지를 수신하도록 선택할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 스트리밍 처리량 용량 경고 | 세 가지 새로운 경고를 통해 사용자는 경고를 구독하고 구성하여 스트리밍 처리량 용량의 성능을 사전에 관리하고 모니터링할 수 있습니다. 스트리밍 처리량이 80%, 90%에 도달하거나 용량 한도를 초과하는 경우 새로운 경고가 제공됩니다. 자세한 내용은 [용량 경고 규칙](../../observability/alerts/rules.md#capacity) 안내서를 참조하십시오. |

경고에 대한 자세한 내용은 [[!DNL Observability Insights] 개요](../../observability/home.md)를 참조하십시오.

## 카탈로그 서비스 {#catalog-service}

카탈로그 서비스는 Adobe Experience Platform 내의 데이터 위치 및 계보에 대한 레코드 시스템입니다. Experience Platform에 수집된 모든 데이터는 데이터 레이크에 파일 및 디렉터리로 저장되지만 카탈로그는 조회 및 모니터링 목적으로 해당 파일 및 디렉터리에 대한 메타데이터와 설명을 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 실시간 고객 프로필에 대한 데이터 보존 | 실시간 고객 프로필의 데이터 보존 기간은 30일에 **한 번만** 업데이트할 수 있습니다. |

카탈로그 서비스에 대한 자세한 내용은 [카탈로그 서비스 개요](../../catalog/home.md)를 참조하십시오.

## 대상 {#destinations}

[!DNL Destinations]는 대상 플랫폼과의 사전 빌드된 통합을 통해 Experience Platform의 데이터를 원활하게 활성화할 수 있습니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타기팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

>[!IMPORTANT]
>
>**데이터 세트 내보내기 일정 연장**
>
>조직에서 2024년 11월 이전에 생성된 데이터 세트 내보내기 데이터 흐름이 있는 경우, 해당 데이터 흐름은 **2025년 9월 1일**&#x200B;부터 작동을 중단합니다. 2025년 9월 1일 이후에도 데이터를 계속 내보내는 데 데이터 흐름이 필요한 경우, [이 안내서](../../destinations/ui/dataset-expiration-update.md)의 단계를 따라 데이터 세트를 내보내는 각 대상에 대한 일정을 연장해야 합니다.

>[!IMPORTANT]
>
>**IP API 기반 대상에 대한 허용 목록 업데이트가 필요합니다.**
>
>스트리밍 대상 내보내기 엔진이 업그레이드되었으므로 API 기반 대상에 대한 [IP 허용 목록](../../destinations/catalog/streaming/ip-address-allow-list.md)을 사용하는 조직은 **2025년 9월 15일 이전**&#x200B;까지 다음 IP 주소를 허용 목록에 추가해야 합니다.
>
>**IP 주소는 필수 항목입니다.**
>
>```
>3.209.222.108
>3.211.230.204
>35.169.227.49
>66.117.18.133
>66.117.18.134
>66.117.18.135
>```
>
>**이 변경 사항은 다음 대상 유형에 적용됩니다.**
>
>- [스트리밍 대상자 내보내기 대상](../../destinations/destination-types.md#streaming-destinations) ([Pega CDH 실시간 대상자](/help/destinations/catalog/personalization/pega-v2.md), [Salesforce Marketing Cloud](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md) 및 [Oracle Eloqua](../../destinations/catalog/email-marketing/oracle-eloqua-api.md)와의 API 기반 통합)
>- [Destination SDK](../../destinations/destination-sdk/getting-started.md)를 통해 빌드된 공개 또는 비공개 대상
>
>**필요한 액션:** API 기반 스트리밍 대상에 IP 주소를 허용 목록에 추가하기 위해 Adobe와 협력한 경우, API 기반 대상에 대한 중단 없는 데이터 흐름을 보장하려면 위의 IP 주소를 허용 목록에 추가해야 합니다.

**새로운 대상**

| 대상 | 설명 |
| --- | --- |
| [[!DNL Acxiom Real ID Audience Connection]](../../destinations/catalog/advertising/acxiom-real-id-audience-connection.md) 대상 | [!DNL Acxiom Real ID Audience Connection] 대상을 사용하여 [!DNL Acxiom's] [Real ID](https://www.acxiom.com/real-id/real-id/) 기술을 통해 대상자를 개선하고, 다양한 플랫폼(예: [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] 등)으로 대상자를 활성화하십시오. |

**업데이트된 대상**

| 대상 | 설명 |
| --- | --- |
| [[!DNL Microsoft Bing]](../../destinations/catalog/advertising/bing.md) 내부 업그레이드 | 2025년 8월 11일부터 짧은 기간 동안 대상 카탈로그에서 두 장의 **[!DNL Microsoft Bing]** 카드가 나란히 표시되었습니다. 이는 대상 서비스의 내부 업그레이드로 인한 변경 사항입니다. 기존 **[!DNL Microsoft Bing]** 대상 커넥터의 이름이 **[!UICONTROL (Deprecated) Microsoft Bing]**(으)로 변경되었으며 이름이 **[!UICONTROL Microsoft Bing]**&#x200B;인 새 카드를 사용할 수 있습니다. <br> 업그레이드가 완료되었으며, 더 이상 사용되지 않는 카드는 대상 카탈로그에서 제거되었습니다. 새 활성화 데이터 흐름에 대해 카탈로그의 **[!UICONTROL Microsoft Bing]** 연결을 사용하십시오. **[!UICONTROL (Deprecated) Microsoft Bing]** 대상에 대한 활성 데이터 흐름이 있는 경우 자동으로 업데이트되므로 사용자의 작업이 필요하지 않습니다. <br><br>[Flow Service API](https://developer.adobe.com/experience-platform-apis/references/destinations/)를 통해 데이터 흐름을 생성하는 경우 [!DNL flow spec ID]및 [!DNL connection spec ID]를 다음 값으로 업데이트해야 합니다.<ul><li>흐름 사양 ID: `8d42c81d-9ba7-4534-9bf6-cf7c64fbd12e`</li><li>연결 사양 ID: `dd69fc59-3bc5-451e-8ec2-1e74a670afd4`</li></ul> 이 업그레이드를 적용하면 [!DNL Microsoft Bing]에 대한 데이터 흐름에서 **활성화된 프로필 수가 감소**&#x200B;할 수 있습니다. 이러한 감소는 이 대상 플랫폼에 대한 모든 활성화의 **ECID 매핑 요구 사항** 도입으로 인해 발생합니다. |
| [[!DNL LinkedIn]](../../destinations/catalog/social/linkedin.md) 및 [LinkedIn 일치 대상자](../../destinations/catalog/social/linkedin-b2b.md) 대상에 대한 인증 만료 세부 정보 | [!DNL LinkedIn] 대상에 대한 인증 만료 정보가 이제 Experience Platform 인터페이스에 직접 표시되므로 데이터 흐름이 중단되기 전에 인증이 만료되고 갱신되는 시점을 확인할 수 있습니다. **[!UICONTROL Account expiration date]** 또는 **[[!UICONTROL Accounts]](../../destinations/ui/destinations-workspace.md#accounts)** 탭의 **[[!UICONTROL Browse]](../../destinations/ui/destinations-workspace.md#browse)** 열에서 토큰 만료 날짜를 모니터링할 수 있습니다. |
| [일치하는 대상](../../destinations/catalog/social/linkedin-b2b.md) [!DNL IDFA] ID 지원 제거 | [!DNL IDFA]은(는) [!DNL IDFA] 대상에서 더 이상 지원되지 않으므로 2025년 9월부터는 [!DNL LinkedIn Matched Audiences]을(를) 대상 ID로 매핑할 수 없습니다. 자세한 내용은 [!DNL LinkedIn Matched Audiences] 통합 [설명서](https://learn.microsoft.com/en-us/linkedin/marketing/matched-audiences/create-and-manage-segment-users?view=li-lms-2025-07&tabs=http#idtypes)를 참조하세요. 이 변경은 LinkedIn의 요구 사항에 기인하며, Experience Platform 대상 서비스 업그레이드와는 관련이 없습니다. |

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 대상에 대한 향상된 검색, 필터링 및 태그 지정 기능 | [찾아보기](../../destinations/ui/destinations-workspace.md#browse) 및 [계정](../../destinations/ui/destinations-workspace.md#accounts) 탭에서 향상된 검색, 필터링 및 태그 지정 기능으로 대상 관리 워크플로를 개선하십시오. <br>이제 이름으로 특정 데이터 흐름과 계정을 검색하고, 대상 플랫폼, 상태, 날짜를 포함한 다양한 기준으로 필터링하고, 대상을 정리하기 위한 사용자 정의 태그를 만들 수 있습니다. 마지막 데이터 흐름 런타임과 같은 주요 필드에 대해서도 열 정렬 기능을 사용할 수 있으므로 대상 연결을 더 쉽게 식별하고 관리할 수 있습니다.<br> ![찾아보기 탭에서 대상 데이터 흐름을 검색하는 애니메이션 데모](../../destinations/assets/ui/workspace/search.gif) |

## 경험 데이터 모델 (XDM) {#xdm}

XDM은 Experience Platform에 가져온 데이터에 대한 공통 구조와 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수하여 모든 고객 경험 데이터를 공통된 표현에 통합해 보다 빠르고 통합된 방식으로 인사이트를 제공할 수 있습니다. 고객 조치에서 귀중한 인사이트를 얻고, 세그먼트를 통해 고객 대상자를 정의하고, 개인 설정 목적으로 고객 속성을 사용할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 관계형 스키마 | 관계형 스키마(이전의 모델 기반 스키마)를 사용하여 데이터 모델링을 단순화합니다. 이제 포괄적인 방법 예제와 지침을 통해 스키마를 더 쉽게 만들 수 있습니다. 이 기능은 현재 캠페인 오케스트레이션 라이선스 보유자에게만 제공되며, 정식 출시 후에는 GA의 Data Distiller 고객에게도 확장되어 데이터 모델링의 접근성과 효율성이 향상될 예정입니다. |

자세한 내용은 [XDM 개요](../../xdm/home.md)를 참조하십시오.

<!--
## Real-Time Customer Profile {#profile}

Real-Time Customer Profile provides a unified, actionable view of each customer by consolidating data from all channels into a single profile.

**New or updated features**

| Feature | Description |
| --- | --- |
| Enhanced lookup functionality in the Entities API | The Entities API now supports the following: <ul><li>Person (Profile)</li><li>Experience Events</li><li>Account</li><li>Opportunity</li></ul> This update simplifies API usage and helps ensure optimal performance and reliability. If you previously used lookups for other entity types—including join tables and custom Multi-Entity types—now is a great opportunity to review your API usage and take advantage of the improved experience. For more information, read the [Real-Time CDB B2B Edition architecture upgrade guide](../../rtcdp/b2b-architecture-upgrade.md). |

For more information on Real-Time Customer Profile, read the [Profile overview](../../profile/home.md).

-->

## 샌드박스 {#sandboxes}

Experience Platform은 전 세계적으로 디지털 체험 애플리케이션을 풍부하게 제공하기 위해 빌드되었습니다. 기업은 여러 디지털 경험 애플리케이션을 동시에 실행하는 경우가 많으며, 운영 규정 준수를 보장하면서 이러한 애플리케이션의 개발, 테스트 및 배포를 처리해야 합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 가져오기 워크플로에서 종속 오브젝트 중복 제거 | 이제 샌드박스 도구는 동일한 이름을 가진 오브젝트가 감지되면 항상 기존 오브젝트를 재사용하여 오브젝트 확산을 방지합니다. 이 변경 사항은 다음 오브젝트에 적용됩니다. <ul><li>스키마</li><li>필드 그룹</li><li>대상자</li><li>`decisioning_ranking`</li><li>`decisioning_rules`</li></ul> 자세한 내용은 [샌드박스 도구에 대해 지원되는 오브젝트에 대한 안내서](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling)를 참조하십시오. |
| 조직 간 패키지 공유를 위한 전체 샌드박스 지원 | 샌드박스 도구는 이제 조직 패키지 공유 전반에서 **전체 샌드박스** 유형을 지원합니다. 이제 조직 전체에서 샌드박스 패키지와 다중 오브젝트 패키지를 모두 공유할 수 있습니다. 자세한 내용은 [샌드박스 도구에 대해 지원되는 오브젝트에 대한 안내서](../../sandboxes/ui/sharing-packages-across-orgs.md)를 참조하십시오. |

샌드박스에 대한 자세한 내용은 [샌드박스 개요](../../sandboxes/home.md)를 참조하십시오.

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service]는 고객 기반 내에서 마케팅 가능한 사용자 그룹을 구분하는 기준을 설명하여 프로필의 특정 하위 집합을 정의합니다. 대상자는 기록 데이터(예: 인구 통계 정보) 또는 고객과 브랜드의 상호 작용을 나타내는 시계열 이벤트를 기반으로 할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 대상자 예상치 | 대상자 예상치는 이제 샘플링 데이터의 신뢰 구간을 기반으로 하는 **범위**&#x200B;로 표시됩니다. 예상치에 대한 자세한 내용은 [세그먼트 빌더 안내서](/help/segmentation/ui/segment-builder.md#audience-properties)를 참조하십시오. |

자세한 내용은 [[!DNL Segmentation Service] 개요](../../segmentation/home.md)를 참조하십시오.

## 소스 {#sources}

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [!DNL Oracle NetSuite] 소스의 일반 가용성 | 이제 [!DNL Oracle NetSuite] 소스를 일반적으로 사용할 수 있습니다. 이제 [!DNL Oracle NetSuite] 계정을 Experience Platform에 연결하여 활동 및 엔티티 데이터를 수집하고 통합 분석 및 활성화를 수행할 수 있습니다. 자세한 내용은 [[!DNL Oracle NetSuite] 개요](../../sources/connectors/marketing-automation/oracle-netsuite.md)를 참조하십시오. |
| [!DNL PathFactory] 소스의 일반 가용성 | 이제 [!DNL PathFactory] 소스를 일반적으로 사용할 수 있습니다. 통합 분석 및 활성화를 위해 [!DNL PathFactory] 계정을 Experience Platform에 연결하여 방문자, 세션 및 페이지 조회수 데이터를 수집할 수 있습니다. 자세한 내용은 [[!DNL PathFactory] 개요](../../sources/connectors/marketing-automation/pathfactory.md)를 참조하십시오. |
| [!DNL Stripe] 소스의 일반 가용성 | 이제 [!DNL Stripe] 소스를 일반적으로 사용할 수 있습니다. [!DNL Stripe] 계정을 Experience Platform에 연결하여 결제 및 트랜잭션 데이터를 수집하고 통합 분석 및 활성화를 수행할 수 있습니다. 자세한 내용은 [[!DNL Stripe] 개요](../../sources/connectors/payments/stripe.md)를 참조하십시오. |
| [!DNL Azure Blob Storage]에 대해 향상된 인증 | 이제 서비스 주체 기반 인증을 사용하여 [!DNL Azure Blob Storage] 소스를 Experience Platform에 연결할 수 있습니다. 서비스 주체 기반 인증을 사용하면 보안을 강화하고 자격 증명 순환을 쉽게 하며 계정에 대한 액세스 제어를 보다 세부적으로 제어할 수 있습니다. 자세한 내용은 [[!DNL Azure Blob Storage] 개요](../../sources/connectors/cloud-storage/blob.md)를 참조하십시오. |

자세한 내용은 [소스 개요](../../sources/home.md)를 참조하십시오.

<!--
| [!DNL Marketo] source documentation updates | Get complete visibility into how your [!DNL Marketo] data is transformed when it enters Experience Platform. All field mappings now include detailed explanations of data transformations, so you can understand exactly how your `PersonID` becomes `leadID` and `eventType` becomes `activityType`. |
| [!BADGE Beta]{type=Informative} Support for [!DNL Azure Private Links] in the UI | You can now use [!DNL Azure Private Links] for a select group of sources in the UI. Use this feature to create a private endpoint that which your source can connect to. With private endpoints, you can set up connections and dataflows that bypass the public internet, giving you enhanced security and network isolation for your sensitive data. Support for [!DNL Azure Private Links] is available to the following following sources: <ul><li>[[!DNL Azure Blob Storage]](../../sources/connectors/cloud-storage/blob.md)</li><li>[[!DNL ADLS Gen2]](../../sources/connectors/cloud-storage/adls-gen2.md)</li><li>[[!DNL Azure File Storage]](../../sources/connectors/cloud-storage/azure-file-storage.md)</li><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li></ul> For more information, read the guide on [[!DNL Azure Private Links]](../../sources/tutorials/ui/private-link.md). |

| Enhanced [[!DNL Marketo Engage]](../../destinations/catalog/adobe/marketo-engage-connection.md) destination  | The enhanced [[!DNL Marketo Engage]](../../destinations/catalog/adobe/marketo-engage-connection.md) destination is an upgraded version of the existing [[!DNL (Legacy) (V2) Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md) connector. This new connector brings profile sync capabilities in addition to the existing audience sync capabilities from the legacy connector, providing a tighter integration with [!DNL Marketo Engage]. <br> The [[!DNL (Legacy) (V2) Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md) connector will be deprecated in **March 2026**. To ensure a smooth transition to the new **[[!UICONTROL Marketo Engage]](../../destinations/catalog/adobe/marketo-engage-connection.md)** destination, review the following key points and required actions: <ul><li>All users of the existing **[!UICONTROL (Legacy) (V2) Marketo Engage]** must migrate to the new **[!UICONTROL Marketo Engage]** destination by March 2026.</li><li> **Existing dataflows will not be migrated automatically.** You must [set up a new connection](../../destinations/ui/connect-destination.md) to the new **[!UICONTROL Marketo Engage]** destination and activate your audiences there.</li></ul>|
-->
