---
keywords: Experience Platform;활성화;문제 해결;보호 기능;지침;제한
title: 활성화 데이터에 대한 기본 보호 기능
solution: Experience Platform
product: experience platform
type: Documentation
description: 데이터 활성화 기본 사용 및 속도 제한에 대해 자세히 알아보십시오.
exl-id: a755f224-3329-42d6-b8a9-fadcf2b3ca7b
source-git-commit: 7c1d956e3b6a1314baa13fef823d73d42404516a
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 2%

---

# 활성화 데이터 보호

이 페이지에서는 활성화 동작과 관련된 기본 사용량 및 요금 제한을 제공합니다. 다음 가드레일을 검토할 때 올바른 것으로 간주됩니다. [대상에 연결됨](/help/destinations/ui/connect-destination.md).

>[!NOTE]
>
>* 대부분의 고객은 이러한 기본 제한을 초과하지 않습니다. 사용자 지정 제한에 대해 알아보려면 고객 지원 센터 담당자에게 문의하십시오.
>* 이 문서에 설명된 제한 사항이 지속적으로 개선되고 있습니다. 업데이트를 정기적으로 확인하십시오.
>* 개별 다운스트림 제한 사항에 따라 일부 대상의 가드레일이 이 페이지에 설명된 것보다 더 빡빡할 수 있습니다. 또한 다음을 확인하십시오 [카탈로그](/help/destinations/catalog/overview.md) 데이터를 연결 및 활성화할 대상의 페이지입니다.


## 제한 유형 {#limit-types}

이 문서에는 두 가지 유형의 기본 제한이 있습니다.

* **소프트 제한:** 소프트 제한을 넘어설 수 있지만 소프트 제한은 시스템 성능에 대한 권장 지침을 제공합니다.
* **엄격한 제한:** 엄격한 제한은 절대 최대값을 제공합니다. Experience Platform UI 또는 API에서는 이 제한을 초과할 수 없으며, 이 제한을 초과하면 오류가 반환됩니다.


## 활성화 제한 {#activation-limits}

다음 가드레일은 대상에 대한 실시간 고객 프로필 데이터를 활성화할 때 권장 제한을 제공합니다.

### 일반 정품 인증 보호 {#general-activation-guardrails}

아래의 보호 기능은 일반적으로 다음을 통해 활성화에 적용됩니다. [모든 대상 유형](/help/destinations/destination-types.md#destination-types).

| 가드레일 | 제한 | 제한 유형 | 설명 |
| --- | --- | --- | --- |
| 단일 대상에 대한 최대 세그먼트 수 | 250 | 소프트 | 최대 250개의 세그먼트를 데이터 흐름의 단일 대상에 매핑하는 것이 좋습니다. <br><br> 대상에 대해 250개 이상의 세그먼트를 활성화해야 하는 경우 다음 중 하나를 수행할 수 있습니다. <ul><li> 더 이상 활성화하지 않으려는 세그먼트 매핑 해제 또는</li><li>원하는 대상에 대한 새 데이터 흐름을 만들고 세그먼트를 이 새 데이터 흐름에 매핑합니다.</li></ul> <br> 일부 대상의 경우 대상에 매핑된 세그먼트는 250개 미만으로 제한될 수 있습니다. 이러한 대상은 해당 섹션에서 페이지의 아래에서 더 많이 호출됩니다. |
| 최대 대상 수 | 100 | 소프트 | 데이터를 연결하고 활성화할 수 있는 대상을 최대 100개까지 만드는 것이 좋습니다 *샌드박스당*. [Edge 개인화 대상(사용자 지정 개인화)](#edge-destinations-activation) 는 100개의 권장 대상 중 최대 10개를 구성할 수 있습니다. |
| 대상에 매핑된 최대 속성 수 | 50 | 소프트 | 여러 대상 및 대상 유형의 경우 내보내기 위해 매핑할 프로필 속성 및 ID를 선택할 수 있습니다. 최적의 성능을 위해 데이터 흐름에서 대상에 최대 50개의 속성을 매핑해야 합니다. |
| 대상에 활성화된 데이터 유형 | ID 및 ID 맵을 포함한 프로필 데이터 | 하드 | 현재는 내보내기만 가능합니다 *프로필 레코드 속성* 대상으로 이동합니다. 이벤트 데이터를 설명하는 XDM 속성은 현재 내보내기에서 지원되지 않습니다. |
| 대상에 활성화된 데이터 유형 - 배열 및 맵 속성 지원 | 사용할 수 없음 | 하드 | 현재, **아님** 내보내기 가능 *배열 또는 맵 특성* 대상으로 이동합니다. 이 규칙의 예외는 다음과 같습니다. [id 맵](/help/xdm/field-groups/profile/identitymap.md): 스트리밍과 파일 기반 활성화 모두에서 내보내집니다. |

{style="table-layout:auto"}

### 스트리밍 활성화 {#streaming-activation}

아래 보호 기능은 다음을 통해 활성화에 적용됩니다. [스트리밍 대상](/help/destinations/ui/activate-segment-streaming-destinations.md).

| 가드레일 | 제한 | 제한 유형 | 설명 |
| --- | --- | --- | --- |
| 초당 활성화 수(프로필 내보내기가 있는 HTTP 메시지) | 해당 없음 | - | 현재는 Experience Platform에서 파트너 대상의 API 끝점으로 전송되는 초당 메시지 수에 제한이 없습니다. <br> 제한이나 지연은 Experience Platform이 데이터를 전송하는 엔드포인트에 의해 결정됩니다. 또한 다음을 확인하십시오 [카탈로그](/help/destinations/catalog/overview.md) 데이터를 연결 및 활성화할 대상의 페이지입니다. |

{style="table-layout:auto"}

### 일괄 처리(파일 기반) 활성화 {#batch-file-based-activation}

아래 보호 기능은 다음을 통해 활성화에 적용됩니다. [배치(파일 기반) 대상](/help/destinations/ui/activate-batch-profile-destinations.md).

| 가드레일 | 제한 | 제한 유형 | 설명 |
| --- | --- | --- | --- |
| 활성화 빈도 | 3, 6, 8 또는 12시간마다 일일 전체 내보내기 또는 빈번한 증분 내보내기 | 하드 | 읽기 [전체 파일 내보내기](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) 및 [증분 파일 내보내기](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) 일괄 내보내기의 빈도 증분에 대한 자세한 내용은 설명서 섹션을 참조하십시오. |
| 지정된 시간에 내보낼 수 있는 최대 세그먼트 수 | 100 | 소프트 | 최대 100개의 세그먼트를 배치 대상 데이터 흐름에 추가하는 것이 좋습니다. |
| 활성화할 파일당 최대 행(레코드) 수 | 500만 | 하드 | Adobe Experience Platform은 내보낸 파일을 파일당 5백만 개의 레코드(행)로 자동으로 분할합니다. 각 행은 하나의 프로필을 나타냅니다. 분할 파일 이름에는 다음과 같이 파일이 더 큰 내보내기의 일부임을 나타내는 숫자가 추가됩니다. `filename.csv`, `filename_2.csv`, `filename_3.csv`. 자세한 내용은 [예약 섹션](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) 배치 대상 활성화 자습서 |

{style="table-layout:auto"}

### 임시 활성화 {#ad-hoc-activation}

아래의 보호 기능은 [애드혹 활성화](/help/destinations/api/ad-hoc-activation-api.md) 메서드를 사용합니다.

| 가드레일 | 제한 | 제한 유형 | 설명 |
| --- | --- | --- | --- |
| 애드혹 활성화 작업당 세그먼트 활성화됨 | 80 | 하드 | 현재 각 임시 활성화 작업은 최대 80개의 세그먼트를 활성화할 수 있습니다. 작업당 80개 이상의 세그먼트를 활성화하려고 하면 작업이 실패합니다. 이 동작은 향후 릴리스에서 변경될 수 있습니다. |
| 세그먼트당 동시 임시 활성화 작업 | 1 | 하드 | 세그먼트당 동시 임시 활성화 작업을 두 개 이상 실행하지 마십시오. |

{style="table-layout:auto"}

### Edge 개인화 대상 활성화 {#edge-destinations-activation}

아래 보호 기능은 다음을 통해 활성화에 적용됩니다. [edge 개인화 대상](/help/destinations/destination-types.md#streaming-profile-export).

| 가드레일 | 제한 | 제한 유형 | 설명 |
| --- | --- | --- | --- |
| 최대 수 [사용자 정의 개인화](/help/destinations/catalog/personalization/custom-personalization.md) 대상 | 10 | 소프트 | 샌드박스당 10개의 사용자 지정 개인화 대상으로 데이터 흐름을 설정할 수 있습니다. |
| 샌드박스당 개인화 대상에 매핑된 최대 속성 수 | 30 | 하드 | 샌드박스당 데이터 흐름에서 개인화 대상에 최대 30개의 속성을 매핑할 수 있습니다. |
| 하나에 매핑된 최대 세그먼트 수 [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) 대상 | 50 | 소프트 | 단일 Adobe Target 대상에 대한 활성화 플로우에서 최대 50개의 세그먼트를 활성화할 수 있습니다. |

{style="table-layout:auto"}

### Destination SDK 보호 {#destination-sdk-guardrails}

[Destination SDK](/help/destinations/destination-sdk/overview.md) 는 선택한 데이터 및 인증 형식을 기반으로 Experience Platform에 대한 대상 통합 패턴을 구성하여 대상과 프로필 데이터를 엔드포인트에 전달할 수 있도록 하는 구성 API의 세트입니다. 아래 가드레일은 Destination SDK을 사용하여 구성하는 대상에 적용됩니다.

| 가드레일 | 제한 | 제한 유형 | 설명 |
| --- | --- | --- | --- |
| 최대 수 [비공개 사용자 지정 대상](/help/destinations/destination-sdk/overview.md#productized-custom-integrations) | 5 | 소프트 | Destination SDK을 사용하여 최대 5개의 개인 사용자 지정 스트리밍 또는 일괄 처리 대상을 만들 수 있습니다. 이러한 대상을 5개 이상 만들어야 하는 경우 사용자 정의 지원 담당자에게 문의하십시오. |
| Destination SDK에 대한 프로필 내보내기 정책 | <ul><li>`maxBatchAgeInSecs` (최소 1.800 및 최대 3.600)</li><li>`maxNumEventsInBatch` (최소 1.000, 최대 10.000)</li></ul> | 하드 | 사용 시 [구성 가능한 집계](destination-sdk/functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) 대상에 대한 옵션은 API 기반 대상으로 HTTP 메시지를 보내는 빈도와 메시지에 포함되어야 하는 프로필의 수를 결정하는 최소값과 최대값을 염두에 두어야 합니다. |

{style="table-layout:auto"}

### 대상 제한 및 다시 시도 정책 {#destination-throttling-and-retry-policy}

특정 대상에 대한 임계값 제한 또는 제한에 대한 세부 사항입니다. 이 섹션에서는 대상에 대한 재시도 정책에 대한 정보도 제공합니다.

| 대상 유형 | 설명 |
| --- | --- |
| 엔터프라이즈 대상(HTTP API, Amazon Kinesis, Azure EventHubs) | 95% 의 시간 동안 Experience Platform은 성공적으로 전송된 메시지에 대해 10분 미만의 처리량 지연 시간을 제공하려고 시도하며, 엔터프라이즈 대상으로 전송되는 각 데이터 흐름당 초당 요청 수가 10,000건 미만입니다. <br> Enterprise 대상에 대한 요청이 실패한 경우 Experience Platform은 실패한 요청을 저장하고 두 번 다시 시도하여 요청을 끝점으로 보냅니다. |

{style="table-layout:auto"}

## 기타 Experience Platform 서비스 보호 {#guardrails-other-services}

다른 Experience Platform 서비스에 대한 보호 정보 보기:

* 의 보호 기능 [데이터 수집](/help/ingestion/guardrails.md)
* 의 보호 기능 [[!DNL Identity Service] 데이터](/help/identity-service/guardrails.md)
* 의 보호 기능 [[!DNL Real-Time Customer Profile] 데이터](/help/profile/guardrails.md)
* 의 보호 기능 [[!DNL Query Service] 데이터](/help/query-service/guardrails.md)
