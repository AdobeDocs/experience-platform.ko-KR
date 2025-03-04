---
keywords: Experience Platform;활성화;문제 해결;보호;지침;제한
title: 데이터 활성화를 위한 기본 보호 기능
solution: Experience Platform
product: experience platform
type: Documentation
description: 데이터 활성화 기본 사용 및 속도 제한에 대해 자세히 알아보십시오.
exl-id: a755f224-3329-42d6-b8a9-fadcf2b3ca7b
source-git-commit: 2d640b282feb783694276c69366b1fccadddfd78
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 2%

---

# 데이터 활성화 보호

>[!IMPORTANT]
>
>이 보호 기능 페이지 외에 실제 사용 제한에 대해 판매 주문에서 라이선스 자격 및 해당 [제품 설명](https://helpx.adobe.com/legal/product-descriptions.html)을(를) 확인하십시오.

이 페이지에서는 활성화 동작과 관련된 기본 사용량 및 요금 제한을 제공합니다. 다음 보호 기능을 검토할 때 [대상에 올바르게 연결](/help/destinations/ui/connect-destination.md)되어 있다고 가정합니다.

>[!NOTE]
>
>* 대부분의 고객은 이러한 기본 제한을 초과하지 않습니다. 사용자 지정 제한에 대해 알아보려면 고객 지원 센터 담당자에게 문의하십시오.
>* 이 문서에 설명된 제한 사항이 지속적으로 개선되고 있습니다. 정기적으로 업데이트를 확인하십시오.
>* 개별 다운스트림 제한 사항에 따라 일부 대상의 가드레일이 이 페이지에 설명된 것보다 더 빡빡할 수 있습니다. 데이터를 연결하고 활성화할 대상의 [카탈로그](/help/destinations/catalog/overview.md) 페이지도 확인하십시오.

## 보호 유형 {#limit-types}

이 문서에는 두 가지 유형의 기본 제한이 있습니다.

| 보호 유형 | 설명 |
|----------|---------|
| **성능 보호(소프트 제한)** | 성능 보호는 사용 사례의 범위와 관련된 사용 제한입니다. 성능 가드레일을 초과하면 성능 저하 및 지연이 발생할 수 있습니다. Adobe은 이러한 성능 저하에 대한 책임이 없습니다. 성능 가드레일을 지속적으로 초과하는 고객은 성능 저하를 방지하기 위해 추가 용량의 라이센스를 선택할 수 있습니다. |
| **시스템 적용 보호 기능(하드 제한)** | 시스템에서 적용되는 가드레일은 Real-Time CDP UI 또는 API에 의해 적용됩니다. 이는 UI 및 API가 귀하를 차단하거나 오류를 반환하므로 초과할 수 없는 제한입니다. |

{style="table-layout:auto"}


## 활성화 제한 {#activation-limits}

다음 가드레일은 대상에 대한 실시간 고객 프로필 데이터를 활성화할 때 권장 제한을 제공합니다.

### 일반 정품 인증 보호 {#general-activation-guardrails}

아래의 보호 기능은 일반적으로 [모든 대상 유형](/help/destinations/destination-types.md#destination-types)을 통한 활성화에 적용됩니다.

| 가드레일 | 제한 | 제한 유형 | 설명 |
| --- | --- | --- | --- |
| 단일 대상에 대한 최대 대상 수 | 250 | 성능 보호 | 최대 250개의 대상을 데이터 흐름의 단일 대상에 매핑하는 것이 좋습니다. <br><br> 대상에 대해 250개 이상의 대상을 활성화해야 하는 경우 다음 중 하나를 수행할 수 있습니다. <ul><li> 더 이상 활성화하지 않으려는 대상자 매핑 해제 또는</li><li>원하는 대상에 대한 새 데이터 흐름을 만들고 대상을 이 새 데이터 흐름에 매핑합니다.</li></ul> <br> 일부 대상의 경우 대상에 매핑된 대상자가 250명 미만으로 제한될 수 있습니다. 이러한 대상은 해당 섹션에서 페이지의 아래에서 더 많이 호출됩니다. |
| 대상에 매핑된 최대 속성 수 | 50 | 성능 보호 | 여러 대상 및 대상 유형의 경우 내보내기 위해 매핑할 프로필 속성 및 ID를 선택할 수 있습니다. 최적의 성능을 위해 데이터 흐름에서 대상에 최대 50개의 속성을 매핑해야 합니다. |
| 최대 대상 수 | 10 | 시스템 강제 보호 | 데이터를 연결하고 활성화할 수 있는 대상을 최대 100개까지 만들 수 있습니다. *샌드박스당*. [Edge 개인화 대상(사용자 지정 개인화)](#edge-destinations-activation)은(는) 100개의 권장 대상 중 최대 10개를 구성할 수 있습니다. |
| 대상에 활성화된 데이터 유형 | ID 및 ID 맵을 포함한 프로필 데이터 | 시스템 강제 보호 | 현재 *프로필 레코드 특성*&#x200B;을(를) 대상으로 내보낼 수만 있습니다. 이벤트 데이터를 설명하는 XDM 속성은 현재 내보내기에서 지원되지 않습니다. |
| 대상에 활성화된 데이터 유형 - 배열 및 맵 속성 지원 | 부분적으로 사용 가능하 | 시스템 강제 보호 | 배열 특성을 [파일 기반 대상](/help/destinations/destination-types.md#file-based)(으)로 내보낼 수 있습니다. 기능에 대해 [자세히 알아보십시오](/help/destinations/ui/export-arrays-maps-objects.md). |

{style="table-layout:auto"}

### 스트리밍 활성화 {#streaming-activation}

아래의 보호 기능은 [스트리밍 대상](/help/destinations/ui/activate-segment-streaming-destinations.md)을 통해 활성화되는 데 적용됩니다.

| 가드레일 | 제한 | 제한 유형 | 설명 |
| --- | --- | --- | --- |
| 초당 활성화 수(프로필 내보내기가 있는 HTTP 메시지) | N/A | - | 현재 Experience Platform에서 파트너 대상의 API 엔드포인트로 전송되는 초당 메시지 수에 제한이 없습니다. <br> 제한 또는 지연은 Experience Platform에서 데이터를 보내는 끝점에 의해 결정됩니다. 데이터를 연결하고 활성화할 대상의 [카탈로그](/help/destinations/catalog/overview.md) 페이지도 확인하십시오. |

{style="table-layout:auto"}

### 일괄 처리(파일 기반) 활성화 {#batch-file-based-activation}

[일괄 처리(파일 기반) 대상](/help/destinations/ui/activate-batch-profile-destinations.md)을 통한 활성화에는 아래 보호 기능이 적용됩니다.

| 가드레일 | 제한 | 제한 유형 | 설명 |
| --- | --- | --- | --- |
| 활성화 빈도 | 3, 6, 8 또는 12시간마다 일일 전체 내보내기 또는 빈번한 증분 내보내기 | 시스템 강제 보호 | 일괄 내보내기의 빈도 증가에 대한 자세한 내용은 [전체 파일 내보내기](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) 및 [증분 파일 내보내기](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) 설명서 섹션을 참조하십시오. |
| 지정된 시간에 내보낼 수 있는 최대 대상 수 | 100 | 성능 보호 | 최대 100개의 대상을 대상 데이터 흐름을 일괄 처리하는 것이 좋습니다. |
| 활성화할 파일당 최대 행(레코드) 수 | 500만 | 시스템 강제 보호 | Adobe Experience Platform은 내보낸 파일을 파일당 5백만 개의 레코드(행)로 자동으로 분할합니다. 각 행은 하나의 프로필을 나타냅니다. 분할 파일 이름에는 파일이 더 큰 내보내기의 일부임을 나타내는 숫자가 추가됩니다(예: `filename.csv`, `filename_2.csv`, `filename_3.csv`). 자세한 내용은 일괄 처리 대상 활성화 자습서의 [예약 섹션](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling)을 참조하세요. |

{style="table-layout:auto"}

### 임시 활성화 {#ad-hoc-activation}

아래 보호 기능은 [임시 활성화](/help/destinations/api/ad-hoc-activation-api.md) 메서드에 적용됩니다.

| 가드레일 | 제한 | 제한 유형 | 설명 |
| --- | --- | --- | --- |
| 임시 활성화 작업당 대상자 활성화됨 | 80 | 시스템 강제 보호 | 현재 각 임시 활성화 작업은 최대 80개의 대상을 활성화할 수 있습니다. 작업당 80개 이상의 대상을 활성화하려고 하면 작업이 실패합니다. 이 동작은 향후 릴리스에서 변경될 수 있습니다. |
| 대상당 동시 임시 활성화 작업 | 1 | 시스템 강제 보호 | 대상자당 두 개 이상의 동시 임시 활성화 작업을 실행하지 마십시오. |

{style="table-layout:auto"}

### Edge 개인화 대상 활성화 {#edge-destinations-activation}

아래 가드레일은 [에지 개인화 대상](/help/destinations/destination-types.md#advanced-enterprise-destinations)을 통해 활성화하는 데 적용됩니다.

| 가드레일 | 제한 | 제한 유형 | 설명 |
| --- | --- | --- | --- |
| 최대 [사용자 지정 개인화](/help/destinations/catalog/personalization/custom-personalization.md) 대상 수 | 10 | 성능 보호 | 샌드박스당 10개의 사용자 지정 개인화 대상으로 데이터 흐름을 설정할 수 있습니다. |
| 샌드박스당 개인화 대상에 매핑된 최대 속성 수 | 30 | 시스템 강제 보호 | 샌드박스당 데이터 흐름에서 개인화 대상에 최대 30개의 속성을 매핑할 수 있습니다. |
| 단일 [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) 대상에 매핑된 최대 대상 수 | 50 | 성능 보호 | 단일 Adobe Target 대상에 대한 활성화 흐름에서 최대 50개의 대상을 활성화할 수 있습니다. |

{style="table-layout:auto"}

### 데이터 세트 내보내기 {#dataset-exports}

데이터 세트 내보내기는 현재 **[!UICONTROL 첫 번째 전체 다음 증분]** [패턴](/help/destinations/ui/export-datasets.md#scheduling)에서 지원됩니다. 데이터 집합 내보내기 워크플로우가 설정된 후 발생하는 첫 번째 전체 내보내기에 *이 섹션에 설명된 보호 기능이 적용됩니다*.

<!--

| Guardrail | Limit | Limit Type | Description |
| --- | --- | --- | --- |
| Size of exported datasets | 5 billion records | Soft | The limit described here for dataset exports is a *soft guardrail*. For example, while the user interface will not block you from exporting datasets larger than 5 billion records, the behavior is unpredictable and exports might either fail or have very long export latency. |

{style="table-layout:auto"}

-->

#### 데이터 세트 유형 {#dataset-types}

아래 설명된 대로 Experience Platform에서 내보낸 두 가지 유형의 데이터 세트에 데이터 세트 내보내기 가드레일이 적용됩니다.

**XDM 경험 이벤트 스키마를 기반으로 한 데이터 세트**
XDM 경험 이벤트 스키마를 기반으로 하는 데이터 세트의 경우 데이터 세트 스키마에 최상위 *타임스탬프* 열이 포함됩니다. 데이터는 추가 전용 방식으로 수집됩니다.

**XDM 개별 프로필 스키마를 기반으로 하는 데이터 세트**
XDM 개인 프로필 스키마를 기반으로 하는 데이터 세트의 경우 데이터 세트 스키마에 최상위 *타임스탬프* 열이 포함되지 않습니다. 데이터는 업데이트 방식으로 수집됩니다.

아래의 소프트 가드레일은 Experience Platform에서 내보낸 모든 데이터 세트에 적용됩니다. 또한 다른 데이터 세트 및 압축 유형에 해당하는 하드 가드레일을 아래에서 검토하십시오.

| 가드레일 | 제한 | 제한 유형 | 설명 |
| --- | --- | --- | --- |
| 내보낸 데이터 세트 크기 | 50억 개의 레코드 | 성능 보호 | 데이터 세트 내보내기에 대해 여기에 설명된 제한은 *소프트 가드레일*&#x200B;입니다. 예를 들어, 사용자 인터페이스는 50억 개 이상의 레코드를 내보내는 것을 차단하지 않지만 동작은 예측할 수 없으며 내보내기에 실패하거나 내보내기 지연 시간이 매우 길 수 있습니다. |

{style="table-layout:auto"}

#### 예약된 데이터 세트 내보내기 보호

예약되거나 반복되는 데이터 세트 내보내기의 경우, 아래 가드레일은 내보낸 파일의 두 형식(JSON 또는 Parquet)에 대해 동일하며 데이터 세트 유형별로 그룹화됩니다.

>[!WARNING]
>
>JSON 파일로 내보내기는 압축 모드에서만 지원됩니다.

| 데이터 세트 유형 | 가드레일 | 보호 유형 | 설명 |
---------|----------|---------|-------|
| **XDM 경험 이벤트 스키마**&#x200B;를 기반으로 하는 데이터 세트 | 최근 365일 데이터 | 시스템 강제 보호 | 지난 달력 연도의 데이터를 내보냅니다. |
| **XDM 개별 프로필 스키마**&#x200B;를 기반으로 하는 데이터 세트 | 데이터 흐름의 내보낸 모든 파일에 대해 100억 개의 레코드 보유 | 시스템 강제 보호 | 데이터 세트의 기록 수는 압축된 JSON 또는 Parquet 파일의 경우 100억 개 미만이어야 하고, 압축되지 않은 Parquet 파일의 경우 100만 개 미만이어야 합니다. 그렇지 않으면 내보내기에 실패합니다. 허용된 임계값보다 큰 경우 내보내려는 데이터 세트의 크기를 줄이십시오. |

{style="table-layout:auto"}

<!--

#### Ad-hoc dataset exports

Exporting datasets in an-hoc manner is currently supported via API only. For ad-hoc dataset exports, you must use the backfill parameter in the API to limit the timeframe of exported data. 

The guardrails below are the same whether you are exporting parquet of JSON files ad-hoc. 

**Parquet and JSON output**

|Dataset type | Backfill parameter provided | Guardrail | Guardrail type | Description |
|---------|---------|-----------|-----------|------------|
| Datasets based on the **XDM Experience Events schema** |  <p><ul><li>Both start and end date provided in `backfill` parameter in API call</li><li>Incomplete `backfill` parameter provided in API call</li></ul></p> | <p><ul><li>Last 30 days</li><li>Last 365 days</li></ul></p> | Hard | <p><ul><li>The export fails if the `startDate - endDate` interval is over 30 days</li><li>Either the `startDate` or `endDate` are missing or  incorrectly formatted in the API call. Expected format: `yyyy-MM-dd'T'HH:mm:ss.SSS'Z'`</li></ul></p> |
| Datasets based on the **XDM Individual Profile schema** |  - | Ten billion records across all files exported in a dataflow | Hard | The record count of the dataset must be less than ten billion for compressed JSON or parquet files and one million for uncompressed parquet files, otherwise the export fails. Reduce the size of the dataset that you are trying to export if it is larger than the allowed threshold. |

{style="table-layout:auto"}

-->

[데이터 세트 내보내기](/help/destinations/ui/export-datasets.md)에 대해 자세히 알아보세요.


### Destination SDK 보호 기능 {#destination-sdk-guardrails}

[Destination SDK](/help/destinations/destination-sdk/overview.md)은(는) 선택한 데이터 및 인증 형식을 기반으로 대상과 프로필 데이터를 엔드포인트에 전달하도록 Experience Platform에 대한 대상 통합 패턴을 구성할 수 있는 구성 API 세트입니다. 아래 가드레일은 Destination SDK을 사용하여 구성하는 대상에 적용됩니다.

| 가드레일 | 제한 | 제한 유형 | 설명 |
| --- | --- | --- | --- |
| 최대 [개인 사용자 지정 대상 수](/help/destinations/destination-sdk/overview.md#productized-custom-integrations) | 5 | 성능 보호 | Destination SDK을 사용하여 최대 5개의 개인 사용자 지정 스트리밍 또는 배치 대상을 만들 수 있습니다. 이러한 대상을 5개 이상 만들어야 하는 경우 사용자 정의 지원 담당자에게 문의하십시오. |
| Destination SDK에 대한 프로필 내보내기 정책 | <ul><li>`maxBatchAgeInSecs`(최소 1,800 및 최대 3,600)</li><li>`maxNumEventsInBatch`(최소 1,000개 및 최대 10,000개)</li></ul> | 시스템 강제 보호 | 대상에 대해 [구성 가능한 집계](destination-sdk/functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) 옵션을 사용할 때는 API 기반 대상으로 HTTP 메시지를 보내는 빈도와 메시지에 포함할 프로필 수를 결정하는 최소값과 최대값을 염두에 두십시오. |

{style="table-layout:auto"}

### 대상 제한 및 다시 시도 정책 {#destination-throttling-and-retry-policy}

특정 대상에 대한 임계값 제한 또는 제한에 대한 세부 사항입니다. 이 섹션에서는 대상에 대한 재시도 정책에 대한 정보도 제공합니다.

| 대상 유형 | 설명 |
| --- | --- |
| 엔터프라이즈 대상(HTTP API, Amazon Kinesis, Azure EventHubs) | 그 중 95% 동안 Experience Platform은 엔터프라이즈 대상으로 전송되는 각 데이터 흐름의 초당 요청 수가 10,000개 미만인 상태로 성공적으로 전송된 메시지에 대해 10분 미만의 처리량 지연 시간을 제공하려고 합니다. <br> Enterprise 대상에 대한 요청이 실패한 경우 Experience Platform은 실패한 요청을 저장하고 두 번 다시 시도하여 끝점에 요청을 보냅니다. |

{style="table-layout:auto"}

## 다음 단계

Real-Time CDP 제품 설명 문서의 기타 Experience Platform 서비스 보호, 종단 간 지연 정보 및 라이선스 정보에 대한 자세한 내용은 다음 설명서를 참조하십시오.

* [Real-Time CDP 보호 기능](/help/rtcdp/guardrails/overview.md)
* 다양한 Experience Platform 서비스에 대한 [전체 지연 다이어그램](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams).
* [Real-Time Customer Data Platform(B2C 에디션 - Prime 및 Ultimate 패키지)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform(B2P - Prime 및 Ultimate 패키지)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform(B2B - Prime 및 Ultimate 패키지)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
