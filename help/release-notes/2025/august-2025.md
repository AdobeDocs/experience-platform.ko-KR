---
title: Adobe Experience Platform 릴리스 노트 2025년 8월
description: Adobe Experience Platform에 대한 2025년 8월 릴리스 정보입니다.
exl-id: d93e98f3-d165-4710-ad1d-2ad3857cd0f8
source-git-commit: cb32846bcbd917f267cba587b60dc323f6bc7d96
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 36%

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

**릴리스 일자: 2025년 8월 19일 수요일**


Adobe Experience Platform의 새로운 기능 및 기존 기능 업데이트:

- [경고](#alerts)
- [카탈로그 서비스](#catalog-service)
- [대상](#destinations)
- [경험 데이터 모델 (XDM)](#xdm)
- [실시간 고객 프로필](#profile)
- [샌드박스](#sandboxes)
- [Segmentation Service](#segmentation-service)
- [소스](#sources)

## 경고 {#alerts}

Experience Platform을 통해 다양한 Experience Platform 활동에 대한 이벤트 기반 알림을 구독할 수 있습니다. Experience Platform 사용자 인터페이스의 [!UICONTROL 경고] 탭을 통해 다양한 경고 규칙을 구독할 수 있으며, 원하는 경우 UI 자체 또는 이메일 알림을 통해 알림 메시지를 수신할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 스트리밍 처리량 용량 경고 | 세 가지 새로운 경고를 통해 사용자는 경고를 구독하고 구성하여 스트리밍 처리량 용량의 성능을 사전 예방적으로 관리 및 모니터링할 수 있습니다. 새로운 경고에는 스트리밍 처리량이 80%, 90%에 도달하거나 용량 제한을 초과하는 경우가 포함됩니다. 자세한 내용은 [용량 경고 규칙](../../observability/alerts/rules.md#capacity) 안내서를 참조하십시오. |

경고에 대한 자세한 내용은 [[!DNL Observability Insights] 개요](../../observability/home.md)를 참조하십시오.

## 카탈로그 서비스 {#catalog-service}

카탈로그 서비스는 Adobe Experience Platform 내의 데이터 위치 및 계보에 대한 레코드 시스템입니다. Experience Platform에 수집된 모든 데이터는 데이터 레이크에 파일 및 디렉터리로 저장되지만 카탈로그는 조회 및 모니터링 목적으로 해당 파일 및 디렉터리에 대한 메타데이터와 설명을 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 실시간 고객 프로필에 대한 데이터 유지 | 실시간 고객 프로필에 대한 데이터 보존 기간을 30일마다 한 번씩 **only** 업데이트할 수 있습니다. |

카탈로그 서비스에 대한 자세한 내용은 [카탈로그 서비스 개요](../../catalog/home.md)를 참조하세요.

## 대상 {#destinations}

[!DNL Destinations]은(는) Experience Platform의 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 빌드된 통합입니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타기팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

>[!IMPORTANT]
>
>**데이터 집합 내보내기 일정 확장**
>
>조직에 2024년 11월 이전에 만들어진 데이터 세트 내보내기 데이터 흐름이 있는 경우 이러한 데이터 흐름은 **2025년 9월 1일**&#x200B;에 작동을 중지합니다. 2025년 9월 1일 이후에도 데이터 흐름을 계속 내보내려면 [이 안내서](../../destinations/ui/dataset-expiration-update.md)의 단계를 따라 데이터 세트를 내보내는 각 대상에 대한 일정을 확장해야 합니다.

>[!IMPORTANT]
>
>API 기반 대상에 필요한 **IP 허용 목록 업데이트**
>
>스트리밍 대상 내보내기 엔진으로 업그레이드되어 API 기반 대상에 대해 [IP 허용 목록](../../destinations/catalog/streaming/ip-address-allow-list.md)을(를) 사용하는 조직은 2025년 9월 15일 이전에 **다음 IP 주소를 허용 목록에 추가해야 합니다**.
>
>**필요한 IP 주소:**
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
>**이 변경 사항은 다음 대상 형식에 적용됩니다.**
>
>- [스트리밍 대상 내보내기 대상](../../destinations/destination-types.md#streaming-destinations)([Pega CDH 실시간 대상](/help/destinations/catalog/personalization/pega-v2.md), [Salesforce Marketing Cloud](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md) 및 [Oracle Eloqua](../../destinations/catalog/email-marketing/oracle-eloqua-api.md)와(과) API 기반 통합)
>- [Destination SDK](../../destinations/destination-sdk/getting-started.md)을(를) 통해 빌드된 공개 또는 개인 대상
>
>**필수 사항:** API 기반 스트리밍 대상에 IP 주소를 매핑하는 Adobe 작업을 수행한 경우 위의 IP 주소를 허용 목록에 추가하다허용 목록에 추가하다 에 추가하여 API 기반 대상에 중단 없는 데이터 흐름을 확인해야 합니다.

**새로운 대상**

| 대상 | 설명 |
| --- | --- |
| [[!DNL Acxiom Real ID Audience Connection]](../../destinations/catalog/advertising/acxiom-real-id-audience-connection.md) 대상 | [!DNL Acxiom Real ID Audience Connection] 대상을 사용하여 [!DNL Acxiom's] [Real ID](https://www.acxiom.com/real-id/real-id/) 기술로 대상을 개선하고 [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] 등과 같은 여러 플랫폼에 대상을 활성화합니다. |

**업데이트된 대상**

| 대상 | 설명 |
| --- | --- |
| [[!DNL Microsoft Bing]](../../destinations/catalog/advertising/bing.md) 내부 업그레이드 | 2025년 8월 11일부터 잠시 동안 대상 카탈로그에서 두 개의 **[!DNL Microsoft Bing]** 카드가 나란히 표시되었을 수 있습니다. 이는 대상 서비스의 내부 업그레이드로 인한 변경 사항입니다. 기존 **[!DNL Microsoft Bing]** 대상 커넥터의 이름이 **[!UICONTROL (더 이상 사용되지 않음) Microsoft Bing]**(으)로 변경되었으며 이제 이름이 **[!UICONTROL Microsoft Bing]**&#x200B;인 새 카드를 사용할 수 있습니다. <br> 업그레이드가 완료되었으며 더 이상 사용되지 않는 카드가 대상 카탈로그에서 제거되었습니다. 새 활성화 데이터 흐름은 카탈로그의 **[!UICONTROL Microsoft Bing]** 연결을 사용하십시오. **[!UICONTROL (더 이상 사용되지 않는) Microsoft Bing]** 대상에 대한 활성 데이터 흐름이 있는 경우 자동으로 업데이트되므로 사용자의 작업이 필요하지 않습니다. <br><br> [Flow Service API](https://developer.adobe.com/experience-platform-apis/references/destinations/)를 통해 데이터 흐름을 생성하는 경우 [!DNL flow spec ID] 및 [!DNL connection spec ID]를 다음 값으로 업데이트해야 합니다.<ul><li>흐름 사양 ID: `8d42c81d-9ba7-4534-9bf6-cf7c64fbd12e`</li><li>연결 사양 ID: `dd69fc59-3bc5-451e-8ec2-1e74a670afd4`</li></ul> 이 업그레이드 후에는 **데이터 흐름에서**&#x200B;활성화된 프로필 수[!DNL Microsoft Bing]이(가) 감소할 수 있습니다. 이 삭제는 이 대상 플랫폼에 대한 모든 활성화에 대한 **ECID 매핑 요구 사항**&#x200B;의 도입으로 인해 발생합니다. |


**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 대상에 대한 검색, 필터링 및 태그 지정 기능 향상 | [찾아보기](../../destinations/ui/destinations-workspace.md#browse) 및 [계정](../../destinations/ui/destinations-workspace.md#accounts) 탭에서 향상된 검색, 필터링 및 태그 지정 기능을 통해 대상 관리 워크플로를 개선합니다. <br> 이제 이름별로 특정 데이터 흐름 및 계정을 검색하고 대상 플랫폼, 상태 및 날짜를 포함한 다양한 기준으로 필터링하고 사용자 지정 태그를 만들어 대상을 구성할 수 있습니다. 마지막 데이터 흐름 실행 시간과 같은 주요 필드에도 열 정렬을 사용할 수 있으므로 대상 연결을 보다 쉽게 식별하고 관리할 수 있습니다. <br> ![찾아보기 탭에서 대상 데이터 흐름을 검색하는 애니메이션 데모](../../destinations/assets/ui/workspace/search.gif) |

## 경험 데이터 모델 (XDM) {#xdm}

XDM은 Experience Platform으로 가져온 데이터에 대한 일반적인 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수하여 모든 고객 경험 데이터를 공통된 표현에 통합해 보다 빠르고 통합된 방식으로 인사이트를 제공할 수 있습니다. 고객 조치에서 귀중한 인사이트를 얻고, 세그먼트를 통해 고객 대상자를 정의하고, 개인 설정 목적으로 고객 속성을 사용할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 모델 기반 스키마 | 모델 기반 스키마를 사용하여 데이터 모델링을 단순화합니다. 이제 포괄적인 사용 방법 예제와 지침을 통해 스키마를 보다 쉽게 만들 수 있습니다. 이 기능은 현재 Campaign Orchestration 라이선스 소유자가 사용할 수 있으며 GA 시점에 데이터 Distiller 고객으로 확장되어 데이터 모델링에 더 쉽게 액세스하고 효율적으로 작업할 수 있습니다. |

자세한 내용은 [XDM 개요](../../xdm/home.md)를 참조하십시오.

## 실시간 고객 프로필 {#profile}

Real-Time Customer Profile은 모든 채널의 데이터를 단일 프로필로 통합하여 각 고객에 대한 통합적이고 실행 가능한 보기를 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 엔티티 API의 조회 기능이 개선되었습니다 | 엔티티 API는 이제 다음을 지원합니다. <ul><li>개인(프로필)</li><li>경험 이벤트</li><li>계정</li><li>기회</li></ul> 이 업데이트는 API 사용을 단순화하고 최적의 성능과 안정성을 보장하는 데 도움이 됩니다. 조인 테이블 및 사용자 지정 다중 엔티티 유형을 포함하여 다른 엔티티 유형에 대해 이전에 조회를 사용한 경우, 이제 API 사용을 검토하고 향상된 경험을 활용할 수 있습니다. 자세한 내용은 [실시간 CDB B2B edition 아키텍처 업그레이드 안내서](../../rtcdp/b2b-architecture-upgrade.md)를 참조하십시오. |

실시간 고객 프로필에 대한 자세한 내용은 [프로필 개요](../../profile/home.md)를 참조하십시오.

## 샌드박스 {#sandboxes}

Experience Platform은 전 세계적으로 디지털 체험 애플리케이션을 풍부하게 제공하기 위해 빌드되었습니다. 기업은 여러 디지털 경험 애플리케이션을 동시에 실행하는 경우가 많으며, 운영 규정 준수를 보장하면서 이러한 애플리케이션의 개발, 테스트 및 배포를 처리해야 합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 가져오기 워크플로우의 종속성 객체 중복 제거 | 이제 샌드박스 툴은 동일한 이름의 객체가 검색되는 경우 항상 기존 객체를 재사용하여 객체의 확산을 방지합니다. 이 변경 사항은 다음 객체에 적용됩니다. <ul><li>스키마</li><li>필드 그룹</li><li>대상자</li><li>`decisioning_ranking`</li><li>`decisioning_rules`</li></ul> 자세한 내용은 [샌드박스 도구에 대해 지원되는 오브젝트에 대한 안내서](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling)를 참조하십시오. |
| 전체 조직 패키지 공유에 대한 전체 샌드박스 지원 | 이제 샌드박스 도구 기능이 전체 조직 패키지 공유에서 **전체 샌드박스** 유형을 지원합니다. 이제 조직 간에 전체 샌드박스 및 다중 오브젝트 패키지를 공유할 수 있습니다. 자세한 내용은 [샌드박스 도구에 대해 지원되는 오브젝트에 대한 안내서](../../sandboxes/ui/sharing-packages-across-orgs.md)를 참조하십시오. |

샌드박스에 대한 자세한 내용은 [샌드박스 개요](../../sandboxes/home.md)를 참조하십시오.

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service]는 고객 기반 내에서 마케팅 가능한 사용자 그룹을 구분하는 기준을 설명하여 프로필의 특정 하위 집합을 정의합니다. 대상자는 기록 데이터(예: 인구 통계 정보) 또는 고객과 브랜드의 상호 작용을 나타내는 시계열 이벤트를 기반으로 할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 대상자 예상 | 이제 대상자 예상 값이 세그먼트 빌더 내에서 자동으로 생성됩니다. 이 값은 대상자를 수정할 때마다 업데이트되며 항상 최신 대상자 규칙을 반영합니다. 또한 예상 값이 샘플링 데이터의 신뢰 구간을 기반으로 하는 **범위**(으)로 표시됩니다. |

자세한 내용은 [[!DNL Segmentation Service] 개요](../../segmentation/home.md)를 참조하십시오.

## 소스 {#sources}

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| UI에서 [!BADGE 에 대한 &#x200B;]{type=Informative}Beta[!DNL Azure Private Links] 지원 | 이제 UI에서 선택한 소스 그룹에 [!DNL Azure Private Links]을(를) 사용할 수 있습니다. 이 기능을 사용하여 소스가 연결할 수 있는 개인 엔드포인트를 만듭니다. 비공개 엔드포인트를 사용하면 공용 인터넷을 우회하는 연결 및 데이터 흐름을 설정할 수 있으므로 민감한 데이터에 대한 향상된 보안 및 네트워크 격리를 제공합니다. [!DNL Azure Private Links]에 대한 지원은 다음 소스에서 사용할 수 있습니다. <ul><li>[[!DNL Azure Blob Storage]](../../sources/connectors/cloud-storage/blob.md)</li><li>[[!DNL ADLS Gen2]](../../sources/connectors/cloud-storage/adls-gen2.md)</li><li>[[!DNL Azure File Storage]](../../sources/connectors/cloud-storage/azure-file-storage.md)</li><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li></ul> 자세한 내용은 [[!DNL Azure Private Links]](../../sources/tutorials/ui/private-link.md)의 안내서를 참조하십시오. |
| [!DNL Azure Blob Storage]에 대한 향상된 인증 | 이제 서비스 사용자 기반 인증을 사용하여 [!DNL Azure Blob Storage] 원본을 Experience Platform에 연결할 수 있습니다. 향상된 보안, 보다 쉬운 자격 증명 순환 및 계정에 대한 보다 세분화된 액세스 제어를 위해 서비스 사용자 기반 인증을 사용하십시오. 자세한 내용은 [[!DNL Azure Blob Storage] 개요](../../sources/connectors/cloud-storage/blob.md)를 참조하십시오. |

자세한 내용은 [소스 개요](../../sources/home.md)를 참조하십시오.

<!--
| [!DNL Marketo] source documentation updates | Get complete visibility into how your [!DNL Marketo] data is transformed when it enters Experience Platform. All field mappings now include detailed explanations of data transformations, so you can understand exactly how your `PersonID` becomes `leadID` and `eventType` becomes `activityType`. |
-->
