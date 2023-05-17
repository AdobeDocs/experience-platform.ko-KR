---
keywords: Experience Platform;활성화;문제 해결;보호 기능;지침;제한
title: 활성화 데이터에 대한 기본 보호 기능
solution: Experience Platform
product: experience platform
type: Documentation
description: 데이터 활성화 기본 사용량 및 비율 제한에 대해 자세히 알아보십시오 .
exl-id: a755f224-3329-42d6-b8a9-fadcf2b3ca7b
source-git-commit: 7c1d956e3b6a1314baa13fef823d73d42404516a
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 2%

---

# 활성화 데이터에 대한 보호 기능

이 페이지에서는 활성화 동작과 관련된 기본 사용량 및 비율 제한을 제공합니다. 다음 보호 기능을 검토할 때 가드레일을 올바르게 사용한다고 가정합니다 [대상에 연결](/help/destinations/ui/connect-destination.md).

>[!NOTE]
>
>* 대부분의 고객은 이러한 기본 제한을 초과하지 않습니다. 사용자 지정 제한에 대해 알아보려면 고객 지원 담당자에게 문의하십시오.
>* 이 문서에 설명된 제한은 지속적으로 개선되고 있습니다. 업데이트를 정기적으로 확인하십시오.
>* 개별 다운스트림 제한 사항에 따라 일부 대상은 이 페이지에 설명된 것보다 더 강력한 보호 기능을 가질 수 있습니다. 또한 다음을 확인하십시오 [카탈로그](/help/destinations/catalog/overview.md) 데이터를 연결 및 활성화할 대상의 페이지입니다.


## 제한 유형 {#limit-types}

이 문서에는 두 가지 유형의 기본 제한이 있습니다.

* **소프트 제한:** 소프트 한도를 넘지 않을 수 있지만, 소프트 한계는 시스템 성능에 대한 권장 지침을 제공합니다.
* **하드 제한:** 하드 제한은 절대 최대값을 제공합니다. Experience Platform UI 또는 API를 사용하여 이 제한을 넘지 않도록 하거나, 이 제한을 초과하는 경우 오류가 반환됩니다.


## 활성화 제한 {#activation-limits}

실시간 고객 프로필 데이터를 대상으로 활성화할 때 권장되는 제한은 다음과 같습니다.

### 일반 활성화 보호 기능 {#general-activation-guardrails}

아래 보호 기능은 일반적으로 를 통해 활성화할 때 적용됩니다 [모든 대상 유형](/help/destinations/destination-types.md#destination-types).

| 가드레일 | 제한 | 제한 유형 | 설명 |
| --- | --- | --- | --- |
| 단일 대상에 대한 최대 세그먼트 수 | 250 | 소프트 | 최대 250개의 세그먼트를 데이터 흐름의 단일 대상에 매핑하는 것이 좋습니다. <br><br> 대상에 250개가 넘는 세그먼트를 활성화해야 하는 경우 다음 중 하나를 수행할 수 있습니다. <ul><li> 더 이상 활성화하지 않을 세그먼트의 매핑을 취소하거나</li><li>새 데이터 흐름을 원하는 대상에 만들고 세그먼트를 이 새 데이터 로드에 매핑합니다.</li></ul> <br> 일부 대상의 경우 대상에 매핑된 세그먼트가 250개 미만으로 제한될 수 있습니다. 이러한 대상은 페이지의 각 섹션에서 아래에 자세히 표시됩니다. |
| 최대 대상 수 | 100 | 소프트 | 연결 및 활성화할 수 있는 최대 100개의 대상을 만드는 것이 좋습니다 *샌드박스 당*. [Edge 개인화 대상(사용자 지정 개인화)](#edge-destinations-activation) 권장 대상 100개 중 최대 10개를 구성할 수 있습니다. |
| 대상에 매핑된 최대 속성 수 | 50 | 소프트 | 여러 대상 및 대상 유형의 경우 내보낼 프로필 속성 및 ID를 선택하여 매핑할 수 있습니다. 최적의 성능을 위해 데이터 플로우에 최대 50개의 속성을 대상에 매핑해야 합니다. |
| 대상에 활성화된 데이터 유형 | ID 및 ID 맵을 포함한 프로필 데이터 | 하드 | 현재 내보내기만 가능합니다 *프로필 레코드 속성* 대상 을 참조하십시오. 현재 이벤트 데이터를 설명하는 XDM 특성은 내보내기에서 지원되지 않습니다. |
| 대상에 활성화된 데이터 유형 - 어레이 및 맵 속성 지원 | 사용할 수 없음 | 하드 | 지금은 **not** 내보낼 수 있음 *배열 또는 맵 속성* 대상 을 참조하십시오. 이 규칙의 예외는 [id 맵](/help/xdm/field-groups/profile/identitymap.md)는 스트리밍 및 파일 기반 활성화에서 모두 내보내집니다. |

{style="table-layout:auto"}

### 스트리밍 활성화 {#streaming-activation}

아래 보호 기능은 를 통해 활성화할 때 적용됩니다 [스트리밍 대상](/help/destinations/ui/activate-segment-streaming-destinations.md).

| 가드레일 | 제한 | 제한 유형 | 설명 |
| --- | --- | --- | --- |
| 초당 활성화 수(프로필 내보내기가 있는 HTTP 메시지) | 해당 없음 | - | 현재 Experience Platform에서 파트너 대상의 API 엔드포인트로 전송되는 초당 메시지 수에 제한이 없습니다. <br> 모든 제한 또는 지연 시간은 Experience Platform이 데이터를 보내는 종단점에 의해 결정됩니다. 또한 다음을 확인하십시오 [카탈로그](/help/destinations/catalog/overview.md) 데이터를 연결 및 활성화할 대상의 페이지입니다. |

{style="table-layout:auto"}

### 배치(파일 기반) 활성화 {#batch-file-based-activation}

아래 보호 기능은 를 통해 활성화할 때 적용됩니다 [배치(파일 기반) 대상](/help/destinations/ui/activate-batch-profile-destinations.md).

| 가드레일 | 제한 | 제한 유형 | 설명 |
| --- | --- | --- | --- |
| 활성화 빈도 | 3, 6, 8 또는 12시간마다 1회 전체 내보내기 또는 그 이상 빈번한 증분 내보내기. | 하드 | 다음 문서를 참조하십시오. [전체 파일 내보내기](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) 및 [증분 파일 내보내기](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) 설명서 섹션에 배치 내보내기에 대한 빈도 증분에 대한 자세한 내용이 나와 있습니다. |
| 주어진 시간에 내보낼 수 있는 최대 세그먼트 수 | 100 | 소프트 | 최대 100개의 세그먼트를 배치 대상 데이터 흐름에 추가하는 것이 좋습니다. |
| 활성화할 파일당 최대 행 수(레코드) | 500만 | 하드 | Adobe Experience Platform은 내보낸 파일을 파일당 500만 개의 레코드(행)로 자동으로 분할합니다. 각 행은 하나의 프로필을 나타냅니다. 파일 이름을 분할하면 파일이 더 큰 내보내기의 일부임을 나타내는 숫자가 추가됩니다. `filename.csv`, `filename_2.csv`, `filename_3.csv`. 자세한 내용은 [예약 섹션](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) 배치 대상 활성화 자습서입니다. |

{style="table-layout:auto"}

### 임시 활성화 {#ad-hoc-activation}

아래 보호 기능은 [ad-hoc 활성화](/help/destinations/api/ad-hoc-activation-api.md) 메서드를 사용합니다.

| 가드레일 | 제한 | 제한 유형 | 설명 |
| --- | --- | --- | --- |
| 임시 활성화 작업별로 활성화된 세그먼트 | 80 | 하드 | 현재 각 임시 활성화 작업은 최대 80개의 세그먼트를 활성화할 수 있습니다. 작업당 80개 이상의 세그먼트를 활성화하려고 하면 작업이 실패합니다. 이 동작은 향후 릴리스에서 변경될 수 있습니다. |
| 세그먼트당 동시 임시 활성화 작업 | 1 | 하드 | 세그먼트당 두 개 이상의 Ad-Hoc 활성화 작업을 실행하지 마십시오. |

{style="table-layout:auto"}

### Edge 개인화 대상 활성화 {#edge-destinations-activation}

아래 보호 기능은 를 통해 활성화할 때 적용됩니다 [edge 개인화 대상](/help/destinations/destination-types.md#streaming-profile-export).

| 가드레일 | 제한 | 제한 유형 | 설명 |
| --- | --- | --- | --- |
| 최대 개수 [사용자 지정 개인화](/help/destinations/catalog/personalization/custom-personalization.md) 대상 | 10 | 소프트 | 데이터 흐름을 샌드박스당 10개의 사용자 지정 개인화 대상으로 설정할 수 있습니다. |
| 샌드박스당 개인화 대상에 매핑된 최대 속성 수 | 30 | 하드 | 데이터 플로우에 있는 최대 30개의 속성을 샌드박스당 개인화 대상에 매핑할 수 있습니다. |
| 단일 세그먼트에 매핑된 최대 세그먼트 수 [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) 대상 | 50 | 소프트 | 활성화 흐름에서 최대 50개의 세그먼트를 단일 Adobe Target 대상으로 활성화할 수 있습니다. |

{style="table-layout:auto"}

### Destination SDK 가드 레일 {#destination-sdk-guardrails}

[Destination SDK](/help/destinations/destination-sdk/overview.md) 는 선택한 데이터 및 인증 형식에 따라 Experience Platform이 대상 및 프로필 데이터를 종단점에 제공할 대상 통합 패턴을 구성할 수 있도록 해주는 구성 API 세트입니다. 아래 보호 기능은 Destination SDK을 사용하여 구성하는 대상에 적용됩니다.

| 가드레일 | 제한 | 제한 유형 | 설명 |
| --- | --- | --- | --- |
| 최대 개수 [개인 사용자 지정 대상](/help/destinations/destination-sdk/overview.md#productized-custom-integrations) | 5 | 소프트 | Destination SDK을 사용하여 최대 5개의 개인 사용자 지정 스트리밍 또는 배치 대상을 만들 수 있습니다. 5개 이상의 그러한 대상을 만들어야 하는 경우 사용자 지정 지원 담당자에게 문의하십시오. |
| Destination SDK에 대한 프로필 내보내기 정책 | <ul><li>`maxBatchAgeInSecs` (최소 1.800 및 최대 3.600)</li><li>`maxNumEventsInBatch` (최소 1.000, 최대 10.000)</li></ul> | 하드 | 를 사용할 때 [구성 가능한 합계](destination-sdk/functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) 대상에 대한 옵션을 고려할 때 API 기반 대상으로 HTTP 메시지를 보내는 빈도와 메시지에 포함해야 하는 프로필 수를 결정하는 최소 및 최대 값을 고려해야 합니다. |

{style="table-layout:auto"}

### 대상 제한 및 다시 시도 정책 {#destination-throttling-and-retry-policy}

지정된 대상에 대한 제한 임계값 또는 제한 세부 정보 이 섹션에서는 대상에 대한 다시 시도 정책에 대한 정보도 제공합니다.

| 대상 유형 | 설명 |
| --- | --- |
| 엔터프라이즈 대상(HTTP API, Amazon Kinesis, Azure EventHub) | 95% 동안 Experience Platform은 각 데이터 흐름에서 엔터프라이즈 대상으로 초당 10,000개 미만의 요청과 함께 성공적으로 전송된 메시지에 대해 10분 미만의 처리량 지연을 제공하기 위해 시도합니다. <br> 엔터프라이즈 대상에 대한 실패한 요청의 경우 Experience Platform은 실패한 요청을 두 번 저장하여 종단점에 요청을 보냅니다. |

{style="table-layout:auto"}

## 다른 Experience Platform 서비스에 대한 보호 기능 {#guardrails-other-services}

다른 Experience Platform 서비스에 대한 보호 정보를 봅니다.

* 보호 기능 [데이터 수집](/help/ingestion/guardrails.md)
* 보호 기능 [[!DNL Identity Service] 데이터](/help/identity-service/guardrails.md)
* 보호 기능 [[!DNL Real-Time Customer Profile] 데이터](/help/profile/guardrails.md)
* 보호 기능 [[!DNL Query Service] 데이터](/help/query-service/guardrails.md)
