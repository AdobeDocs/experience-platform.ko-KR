---
title: Adobe Experience Platform 릴리스 노트 2025년 2월
description: Adobe Experience Platform의 2025년 2월 릴리스 정보.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: b29c63942b00fdf597ebfd3ab105519a6b05a476
workflow-type: tm+mt
source-wordcount: '1378'
ht-degree: 21%

---

# Adobe Experience Platform 릴리스 정보

>[!TIP]
>
>이 릴리스에는 Federated Audience Composition 추가 기능에 대한 개선 사항이 포함되어 있습니다. 자세한 내용은 [Federated Audience Composition 릴리스 정보](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/release-notes)를 참조하세요.

**릴리스 일자: 2025년 2월 18일 수요일**

Adobe Experience Platform의 기존 기능 및 설명서 업데이트:

- [AI 어시스턴트](#ai-assistant)
- [카탈로그 서비스](#catalog-service)
- [데이터 준비](#data-prep)
- [대상](#destinations)
- [소스](#sources)
- [설명서 업데이트](#documentation-updates)
   - [Edge 네트워크 및 허브 비교](#edge)
   - [소스에 대한 확장된 흐름 서비스 API](#flow-service)
   - [샌드박스 도구를 사용하여 객체 구성 백업](#back-up-object-configurations)
   - [샌드박스 툴링을 사용하여 전문가 중심 활성화](#center-of-excellence)
   - [데이터 레이크의 경험 이벤트 데이터 세트 유지](#experience-event-dataset-retention)

## AI 어시스턴트 {#ai-assistant}

Adobe Experience Platform의 AI 어시스턴트는 Adobe 애플리케이션에서 워크플로를 가속화하는 데 사용할 수 있는 대화형 환경입니다. AI 어시스턴트를 사용하여 제품 지식을 더 잘 이해하고, 문제를 해결하거나, 정보를 검색하여 운영 인사이트를 얻을 수 있습니다. AI Assistant는 Experience Platform, Real-Time Customer Data Platform, Adobe Journey Optimizer 및 Customer Journey Analytics을 지원합니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 질문 자동 완성 지원 | 이제 AI Assistant에 질문을 입력할 때 AI Assistant가 제공하는 추천 질문 목록에서 선택할 수 있습니다. 이 기능을 사용하여 AI Assistant를 사용하여 워크플로를 더욱 가속화할 수 있습니다. 자세한 내용은 [AI Assistant에서 질문 자동 완성 사용](../../ai-assistant/ui-guide.md#use-question-autocomplete)에 대한 안내서를 참조하십시오. |
| 데이터 세트 가시성 지원 | 이제 AI Assistant를 사용하여 스토리지 크기 및 행 수 등 특정 데이터 세트 지표에 대한 질문에 답변할 수 있습니다. 데이터 가시성 질문은 특정 기간별로 쿼리를 필터링하는 데 사용할 수 있는 한정자를 지원합니다. 자세한 내용은 [AI Assistant 질문 가이드](../../ai-assistant/questions.md)를 참조하십시오. |

{style="table-layout:auto"}

자세한 내용은 [AI Assistant 개요](../../ai-assistant/home.md)를 참조하십시오.

<!-- | General availability of operational insights | Operational insights in AI Assistant are now in GA. Operational insights refer to answers AI Assistant generates about your metadata objects (attributes, audiences, dataflows, datasets, destinations, journeys, schemas, and sources), including counts, lookups, and lineage impact. Operational insights does not look at any data within the sandbox. For more information, read the [AI Assistant UI guide](../../ai-assistant/ui-guide.md). | -->

## 카탈로그 서비스 {#catalog-service}

카탈로그 서비스는 Adobe Experience Platform 내의 데이터 위치 및 계보에 대한 레코드 시스템입니다. Experience Platform에 수집된 모든 데이터는 데이터 레이크에 파일 및 디렉터리로 저장되지만 카탈로그는 조회 및 모니터링 목적으로 해당 파일 및 디렉터리에 대한 메타데이터와 설명을 제공합니다.

| 기능 | 설명 |
| --- | --- |
| 새 API 엔드포인트 | 새 [카탈로그 서비스 API /v2/dataSets/{DATASET_ID} 끝점](../../catalog/api/update-object.md#patch-v2-notation)을 사용하여 Adobe Experience Platform 데이터 세트 메타데이터를 보다 효율적으로 관리합니다. 시스템에서 누락된 경로 수준을 자동으로 생성하므로 복잡하고 깊이 중첩된 데이터 세트 속성을 쉽게 업데이트하여 시간을 절약하고 수동 단계를 줄이며 오류를 최소화합니다. |

{style="table-layout:auto"}

카탈로그 서비스에 대한 자세한 내용은 [카탈로그 서비스 개요](../../catalog/home.md)를 참조하세요.

## 데이터 준비 {#data-prep}

데이터 준비를 사용하면 데이터 엔지니어가 경험 데이터 모델(XDM)과의 데이터를 매핑, 변환 및 확인할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 매핑 가져오기 및 내보내기에 대한 지원 향상 | 이제 매핑을 CSV 파일로 내보내고 스프레드시트에서 로컬로 구성할 수 있습니다. 그런 다음 UI의 매핑 인터페이스를 사용하여 업데이트된 매핑을 Experience Platform으로 가져올 수 있습니다. 이 기능을 사용하면 UI에서 매핑을 수동으로 빌드하지 않고도 많은 수의 매핑을 구성할 수 있습니다. 또한 새 데이터 흐름을 만들 때 매핑 사본을 Experience Platform에 직접 업로드하여 워크플로를 가속화할 수 있습니다. 자세한 내용은 [매핑 가져오기 및 내보내기](../../data-prep/ui/mapping.md#import-mapping)에 대한 안내서를 참조하십시오. |

{style="table-layout:auto"}

자세한 내용은 [데이터 준비 개요](../../data-prep/home.md)를 참조하십시오.

## 대상 {#destinations}

[!DNL Destinations]는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타기팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 대상 또는 업데이트된 대상** {#new-updated-destinations}

| 대상 | 설명 |
| --- | --- |
| [(Beta) Marketo Engage 사용자 동기화](/help/destinations/catalog/adobe/marketo-engage-person-sync.md) | [!DNL Marketo Engage Person Sync] 커넥터를 사용하여 개인 대상의 업데이트를 [!DNL Marketo Engage] 인스턴스의 해당 레코드로 스트리밍합니다. 이 대상 커넥터는 베타 버전이며 일부 고객만 사용할 수 있습니다. 액세스 권한을 요청하려면 Adobe 담당자에게 문의하십시오. |
| [트레이드 데스크 CRM 연결](/help/destinations/catalog/advertising/tradedesk-emails.md) 일반 가용성 | 이제 [!DNL The Trade Desk CRM] 연결을 일반적으로 사용할 수 있습니다. [!DNL The Trade Desk] CRM 대상을 사용하여 CRM 데이터를 기반으로 대상 타기팅 및 제외를 위해 [!DNL Trade Desk] 계정에 대한 프로필을 활성화합니다. |
| [RainFocus 참석자 프로필 연결](/help/destinations/catalog/marketing-automation/rainfocus.md) | [!DNL RainFocus Attendee Profiles] 대상을 사용하여 참석자 프로필을 만들고 업데이트하려면 Adobe Experience Platform에서 [!DNL RainFocus] 플랫폼으로 고객 프로필을 스트리밍하십시오. |
| [기준 연결](/help/destinations/catalog/advertising/criteo.md) 일반 가용성 | 이제 [!DNL Criteo] 연결을 일반적으로 사용할 수 있습니다. 크리터는 신뢰할 수 있고 영향력 있는 광고를 통해 개방형 인터넷을 통해 모든 소비자에게 더 풍부한 경험을 제공할 수 있도록 지원합니다. 세계 최대 규모의 상거래 데이터 세트와 동급 최고의 AI를 갖춘 Criteo는 쇼핑 여정의 각 접점이 적절한 시간에 적절한 광고를 통해 고객에게 도달하도록 개인화되도록 보장합니다. |
| [[!DNL Amazon Ads] 연결](../../destinations/catalog/advertising/amazon-ads.md) | 이전 베타 버전의 [!DNL Amazon Ads] 커넥터를 이제 일반적으로 사용할 수 있습니다. 커넥터는 또한 개인 데이터를 광고에 사용하기로 동의한 모든 프로필에 대해 동의 승인 신호를 전송하도록 업데이트되었습니다. 새로운 [Amazon 광고 동의 신호](../../destinations/catalog/advertising/amazon-ads.md#destination-details) 컨트롤에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

**새로운 기능 또는 업데이트된 기능** {#destinations-new-updated-functionality}

| 기능 | 설명 |
| --- | --- |
| 액세스 레이블을 사용하여 대상 데이터 흐름에 대한 사용자 액세스 관리 | 이제 Real-Time CDP의 [[!UICONTROL 특성 기반 액세스 제어]](/help/access-control/abac/overview.md) 기능의 일부로 [대상 데이터 흐름](/help/dataflows/ui/monitor-destinations.md)에 액세스 레이블을 적용할 수 있습니다. 이렇게 하면 조직의 일부 사용자만 특정 대상 데이터 흐름에 액세스할 수 있습니다. <br> **중요**: Experience Platform 사용자 인터페이스 상단의 검색 상자를 사용하여 대상 데이터 흐름을 검색할 때 사용자 액세스 레이블에서 볼 수 없도록 제한하는 대상 데이터 흐름이 결과에 포함될 수 있습니다. 이 동작은 향후 업데이트에서 수정될 예정입니다. |
| [Marketo Engage 연결](/help/destinations/catalog/adobe/marketo-engage.md)에 대한 [대상 수준 보고](/help/dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) | 이제 이 대상의 데이터 흐름에 속하는 각 대상에 대해 대상 수준에서 분류된 활성화, 제외 또는 실패한 ID에 대한 정보를 [볼 수 있습니다](/help/dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations). |
| [TikTok](/help/destinations/catalog/social/tiktok.md) 및 [Snap Inc](/help/destinations/catalog/advertising/snap-inc.md) 연결에 대한 외부 대상 지원 | [사용자 지정 업로드](../../segmentation/ui/audience-portal.md#import-audience) 및 [통합 대상 구성](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/audiences)에서 이러한 대상에 대해 외부 대상을 활성화할 수 있습니다. |

{style="table-layout:auto"}

**수정 사항 및 개선 사항** {#destinations-fixes-and-enhancements}

- Destination SDK 테스트 도구의 문제가 수정되었습니다. 프로필 생성에 사용된 스키마에 `No format` 선택기가 있는 데이터 형식이 포함된 경우 지원되지 않는 형식으로 인해 일부 고객 또는 파트너에서 [샘플 프로필 생성 도구](/help/destinations/destination-sdk/testing-api/streaming-destinations/sample-profile-generation-api.md)에 문제가 발생했습니다.
- 흐름 서비스 API를 사용하여 대상의 `targetConnection` 사양을 업데이트할 때 발생하는 문제가 해결되었습니다. 경우에 따라 PATCH 작업이 POST 작업과 유사하게 동작하여 기존 데이터 흐름이 손상됩니다. 이제 이 문제가 해결되었으며 모든 고객은 흐름 서비스 API를 사용하여 `targetConnection` 사양을 업데이트할 수 있습니다. [자세히 보기](/help/destinations/api/edit-destination.md#patch-target-connection).

## 소스 {#sources}

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

Experience Platform의 소스를 사용하여 Adobe 애플리케이션 또는 서드파티 데이터 소스에서 데이터를 수집합니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [!DNL Microsoft Dynamics]에서 보기 지원 | 이제 [!DNL Microsoft Dynamics] 소스를 사용할 때 `"entityType": "view"`을(를) 수집할 수 있습니다. 자세한 내용은 [Experience Platform에  [!DNL Microsoft Dynamics] 소스 연결](../../sources/tutorials/api/create/crm/ms-dynamics.md)에 대한 안내서를 참조하십시오. |

{style="table-layout:auto"}

자세한 내용은 [소스 개요](../../sources/home.md)를 참조하십시오.

## 설명서 업데이트 {#documentation-updates}

### Edge Network 및 허브 비교 {#edge}

[Edge Network과 허브 비교](../../landing/edge-and-hub-comparison.md)에서는 각 서버 유형에서 사용할 수 있는 서비스, 서버 위치 및 각 서버 유형을 사용하기 위한 권장 시나리오를 포함하여 Adobe Experience Platform에 대한 두 서버 유형(hub와 Edge Network) 간의 차이점을 자세히 설명하는 개요를 제공합니다.

### 소스에 대한 확장된 흐름 서비스 API 참조 {#flow-service}

소스에 대한 [[!DNL Flow Service] API 참조](https://developer.adobe.com/experience-platform-apis/references/flow-service/#tag/Source-connections)이(가) 새 API 요청 및 응답 예제로 업데이트되었습니다. 확장된 API 참조를 사용하여 자체 소스를 Experience Platform에 통합할 때 연결 사양을 만들고 업데이트합니다. 확장된 API 참조를 사용하여 소스 엔티티에서 상태 전환을 수행하고, 기존 소스 및 타겟 연결을 업데이트하며, 특정 필터링 기준이 지정된 흐름 및 흐름 사양을 검색할 수도 있습니다.

### 샌드박스 도구를 사용하여 객체 구성 백업 {#back-up-object-configurations}

개체 구성이 저장되고 안전한지 확인하기 위해 샌드박스 도구를 사용하여 백업 패키지를 만드는 방법에 대한 단계별 지침은 [개체 구성 백업 안내서](../../sandboxes/use-cases/backup-object-configuration.md)를 참조하십시오.

### 샌드박스 툴링을 사용하여 전문가 중심 활성화 {#center-of-excellence}

주요 구성을 효율적으로 공유할 수 있는 탁월성의 중심 역할을 하는 &quot;골든 샌드박스&quot; 패키지를 만드는 방법에 대한 단계별 지침은 [우수성의 중심 안내서](../../sandboxes/use-cases/center-of-excellence.md)를 참조하십시오.

### 데이터 레이크의 경험 이벤트 데이터 세트 유지 {#experience-event-dataset-retention}

TTL(Time-To-Live)을 사용하여 Adobe Experience Platform에서 경험 이벤트 데이터 세트 보존을 제어합니다. [이 안내서](../../catalog/datasets/experience-event-dataset-retention-ttl-guide.md)에서는 TTL 설정을 평가, 구성 및 관리하여 오래된 레코드를 자동으로 제거하고, 저장소를 최적화하고, 데이터를 적절한 상태로 유지하는 방법을 안내합니다. 모범 사례, 실제 사용 사례 및 주요 고려 사항을 살펴보고 데이터 수명 주기 관리를 향상시킵니다.
