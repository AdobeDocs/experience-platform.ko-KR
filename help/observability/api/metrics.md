---
keywords: Experience Platform;홈;인기 항목
solution: Experience Platform
title: 지표 API 끝점
topic-legacy: developer guide
description: Observability Insights API를 사용하여 Experience Platform에서 관측성 지표를 검색하는 방법을 알아봅니다.
exl-id: 08d416f0-305a-44e2-a2b7-d563b2bdd2d2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '2054'
ht-degree: 4%

---

# 지표 끝점

관찰 가능한 지표는 Adobe Experience Platform의 다양한 기능에 대한 사용 통계, 내역 트렌드 및 성과 지표에 대한 통찰력을 제공합니다. [!DNL Observability Insights API]의 `/metrics` 종단점을 사용하면 [!DNL Platform]에서 조직의 활동에 대한 지표 데이터를 프로그래밍 방식으로 검색할 수 있습니다.

## 시작하기

이 안내서에 사용된 API 끝점은 [[!DNL Observability Insights] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml)의 일부입니다. 계속하기 전에 [시작하기 안내서](./getting-started.md)에서 관련 설명서에 대한 링크, 이 문서에서 샘플 API 호출 읽기 안내서, 모든 [!DNL Experience Platform] API를 성공적으로 호출하기 위해 필요한 필수 헤더에 대한 중요 정보를 검토하십시오.

## 관찰 가능한 지표 검색

API를 사용하여 지표 데이터를 검색하는 데 지원되는 두 가지 방법이 있습니다.

* [버전 1](#v1):쿼리 매개 변수를 사용하여 지표를 지정합니다.
* [버전 2](#v2):JSON 페이로드를 사용하여 필터를 지정하고 지표에 적용합니다.

### 버전 1 {#v1}

쿼리 매개 변수 사용을 통해 지표를 지정하여 `/metrics` 끝점에 GET 요청을 함으로써 지표 데이터를 검색할 수 있습니다.

**API 형식**

`metric` 매개 변수에 최소 하나의 지표를 제공해야 합니다. 다른 쿼리 매개 변수는 결과 필터링에 대한 선택 사항입니다.

```http
GET /metrics?metric={METRIC}
GET /metrics?metric={METRIC}&metric={METRIC_2}
GET /metrics?metric={METRIC}&id={ID}
GET /metrics?metric={METRIC}&dateRange={DATE_RANGE}
GET /metrics?metric={METRIC}&metric={METRIC_2}&id={ID}&dateRange={DATE_RANGE}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{METRIC}` | 노출할 지표. 단일 호출에서 여러 지표를 결합할 때는 앰퍼샌드(`&`)를 사용하여 개별 지표를 구분해야 합니다. 예: `metric={METRIC_1}&metric={METRIC_2}`. |
| `{ID}` | 지표를 노출하려는 특정 [!DNL Platform] 리소스의 식별자입니다. 이 ID는 사용 중인 지표에 따라 선택 사항이거나 필수 사항이거나 해당되지 않을 수 있습니다. 각 지표에 대해 지원되는 ID(필수 및 선택 사항 모두)를 비롯한 사용 가능한 지표 목록은 [부록](#available-metrics)을 참조하십시오. |
| `{DATE_RANGE}` | 노출할 지표에 대한 날짜 범위(예: `2018-10-01T07:00:00.000Z/2018-10-09T07:00:00.000Z`). |

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/observability/insights/metrics?metric=timeseries.ingestion.dataset.size&metric=timeseries.ingestion.dataset.recordsuccess.count&id=5cf8ab4ec48aba145214abeb&dateRange=2018-10-01T07:00:00.000Z/2019-06-06T07:00:00.000Z \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 제공된 `dateRange` 내에 타임스탬프가 포함된 각 개체 목록과 요청 경로에 지정된 지표에 대한 해당 값을 반환합니다. [!DNL Platform] 리소스의 `id`이 요청 경로에 포함된 경우 결과는 해당 특정 리소스에만 적용됩니다. `id`을(를) 생략하면 IMS 조직 내의 해당 모든 리소스에 결과가 적용됩니다.

```json
{
  "id": "5cf8ab4ec48aba145214abeb",
  "imsOrgId": "{IMS_ORG}",
  "timeseries": {
    "granularity": "MONTH",
    "items": [
      {
        "timestamp": "2019-06-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 1125,
          "timeseries.ingestion.dataset.size": 32320
        }
      },
      {
        "timestamp": "2019-05-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 1003,
          "timeseries.ingestion.dataset.size": 31409
        }
      },
      {
        "timestamp": "2019-04-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 740,
          "timeseries.ingestion.dataset.size": 25809
        }
      },
      {
        "timestamp": "2019-03-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 740,
          "timeseries.ingestion.dataset.size": 25809
        }
      },
      {
        "timestamp": "2019-02-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 390,
          "timeseries.ingestion.dataset.size": 16801
        }
      }
    ],
    "_page": null,
    "_links": null
  },
  "stats": {}
}
```

### 버전 2 {#v2}

페이로드에서 검색할 지표를 지정하여 `/metrics` 끝점에 POST 요청을 함으로써 지표 데이터를 검색할 수 있습니다.

**API 형식**

```http
POST /metrics
```

**요청**

```sh
curl -X POST \
  https://platform.adobe.io/data/infrastructure/observability/insights/metrics \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "start": "2020-07-14T00:00:00.000Z",
        "end": "2020-07-22T00:00:00.000Z",
        "granularity": "day",
        "metrics": [
          {
            "name": "timeseries.ingestion.dataset.recordsuccess.count",
            "filters": [
              {
                "name": "dataSetId",
                "value": "5edcfb2fbb642119194c7d94|5eddb21420f516191b7a8dad",
                "groupBy": true
              }
            ],
            "aggregator": "sum",
            "downsample": "sum"
          },
          {
            "name": "timeseries.ingestion.dataset.dailysize",
            "filters": [
              {
                "name": "dataSetId",
                "value": "5eddb21420f516191b7a8dad",
                "groupBy": false
              }
            ],
            "aggregator": "sum",
            "downsample": "sum"
          }
        ]
      }'
```

| 속성 | 설명 |
| --- | --- |
| `start` | 지표 데이터를 검색할 가장 빠른 날짜/시간입니다. |
| `end` | 지표 데이터를 검색할 최신 날짜/시간입니다. |
| `granularity` | 지표 데이터를 다음으로 나눌 시간 간격을 나타내는 선택적 필드입니다. 예를 들어 `DAY` 값은 `start` 및 `end` 날짜 사이의 각 날짜에 대한 지표를 반환하지만 `MONTH` 값은 대신 월별 지표 결과를 그룹화합니다. 이 필드를 사용할 때는 데이터를 그룹화할 집계 함수를 나타내기 위해 해당 `downsample` 속성도 제공해야 합니다. |
| `metrics` | 검색할 각 지표에 대해 하나씩, 객체의 배열입니다. |
| `name` | 관찰력 통찰력으로 인식되는 지표의 이름. 허용되는 지표 이름의 전체 목록은 [부록](#available-metrics)을 참조하십시오. |
| `filters` | 특정 데이터 세트별로 지표를 필터링할 수 있는 선택적 필드입니다. 이 필드는 다음 속성을 포함하는 각 객체와 함께 객체 배열(각 필터에 대해 하나)입니다. <ul><li>`name`:지표를 필터링할 개체 유형입니다. 현재 `dataSets`만 지원됩니다.</li><li>`value`:하나 이상의 데이터 집합의 ID. 여러 데이터 집합 ID를 단일 문자열로 제공할 수 있으며 각 ID는 세로 막대 문자(`|`)로 구분됩니다.</li><li>`groupBy`:true로 설정된 경우 해당 항목이 지표 결과를 개별적으로 반환해야 하는 여러 데이터 세트를  `value` 나타냄을 나타냅니다. false로 설정하면 해당 데이터 세트에 대한 지표 결과가 함께 그룹화됩니다.</li></ul> |
| `aggregator` | 여러 시리즈 레코드를 단일 결과로 그룹화하는 데 사용할 집계 함수를 지정합니다. 사용 가능한 컨텐츠 집계인에 대한 자세한 내용은 [OpenTSDB 설명서](http://opentsdb.net/docs/build/html/user_guide/query/aggregators.html)를 참조하십시오. |
| `downsample` | 필드를 간격(또는 &quot;버킷&quot;)으로 정렬하여 지표 데이터의 샘플링 비율을 줄이기 위해 집계 함수를 지정할 수 있는 선택적 필드입니다. 다운샘플링 간격은 `granularity` 속성에 의해 결정됩니다. 다운샘플링에 대한 자세한 내용은 [OpenTSDB 설명서](http://opentsdb.net/docs/build/html/user_guide/query/downsampling.html)를 참조하십시오. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적인 응답은 요청에 지정된 지표 및 필터에 대한 결과 데이터를 반환합니다.

```json
{
  "metricResponses": [
    {
      "metric": "timeseries.ingestion.dataset.recordsuccess.count",
      "filters": [
        {
          "name": "dataSetId",
          "value": "5edcfb2fbb642119194c7d94|5eddb21420f516191b7a8dad",
          "groupBy": true
        }
      ],
      "datapoints": [
        {
          "groupBy": {
            "dataSetId": "5edcfb2fbb642119194c7d94"
          },
          "dps": {
            "2020-07-14T00:00:00Z": 44.0,
            "2020-07-15T00:00:00Z": 46.0,
            "2020-07-16T00:00:00Z": 36.0,
            "2020-07-17T00:00:00Z": 50.0,
            "2020-07-18T00:00:00Z": 38.0,
            "2020-07-19T00:00:00Z": 40.0,
            "2020-07-20T00:00:00Z": 42.0,
            "2020-07-21T00:00:00Z": 42.0,
            "2020-07-22T00:00:00Z": 50.0
          }
        },
        {
          "groupBy": {
            "dataSetId": "5eddb21420f516191b7a8dad"
          },
          "dps": {
            "2020-07-14T00:00:00Z": 44.0,
            "2020-07-15T00:00:00Z": 46.0,
            "2020-07-16T00:00:00Z": 36.0,
            "2020-07-17T00:00:00Z": 50.0,
            "2020-07-18T00:00:00Z": 38.0,
            "2020-07-19T00:00:00Z": 40.0,
            "2020-07-20T00:00:00Z": 42.0,
            "2020-07-21T00:00:00Z": 42.0,
            "2020-07-22T00:00:00Z": 50.0
          }
        }
      ],
      "granularity": "DAY"
    },
    {
      "metric": "timeseries.ingestion.dataset.dailysize",
      "filters": [
        {
          "name": "dataSetId",
          "value": "5eddb21420f516191b7a8dad",
          "groupBy": false
        }
      ],
      "datapoints": [
        {
          "groupBy": {},
          "dps": {
            "2020-07-14T00:00:00Z": 38455.0,
            "2020-07-15T00:00:00Z": 40213.0,
            "2020-07-16T00:00:00Z": 31476.0,
            "2020-07-17T00:00:00Z": 43705.0,
            "2020-07-18T00:00:00Z": 33227.0,
            "2020-07-19T00:00:00Z": 34977.0,
            "2020-07-20T00:00:00Z": 36735.0,
            "2020-07-21T00:00:00Z": 36737.0,
            "2020-07-22T00:00:00Z": 43715.0
          }
        }
      ],
      "granularity": "DAY"
    }
  ]
}
```

| 속성 | 설명 |
| --- | --- |
| `metricResponses` | 객체가 요청에 지정된 각 지표를 나타내는 배열입니다. 각 객체에는 필터 구성 및 반환된 지표 데이터에 대한 정보가 포함됩니다. |
| `metric` | 요청에 제공된 지표 중 하나의 이름입니다. |
| `filters` | 지정된 지표에 대한 필터 구성. |
| `datapoints` | 지정된 지표 및 필터의 결과를 나타내는 객체가 있는 배열입니다. 배열의 개체 수는 요청에 제공된 필터 옵션에 따라 달라집니다. 필터를 제공하지 않으면 배열에 모든 데이터 세트를 나타내는 단일 객체만 포함됩니다. |
| `groupBy` | 지표의 `filter` 속성에 여러 데이터 세트가 지정되고 요청에서 `groupBy` 옵션이 true로 설정된 경우 이 개체에는 해당 `dps` 속성이 적용되는 데이터 세트의 ID가 포함됩니다.<br><br>응답에서 이 객체가 비어 있는 것으로 나타나면 해당  `dps` 속성이  `filters` 배열에 제공된 모든 데이터 세트(또는 필터를 제공하지  [!DNL Platform] 않은 경우 모든 데이터 세트)에 적용됩니다. |
| `dps` | 주어진 지표, 필터 및 시간 범위에 대해 반환된 데이터입니다. 이 개체의 각 키는 지정된 지표에 해당하는 값을 가진 타임스탬프를 나타냅니다. 각 데이터 포인트 사이의 기간은 요청에 지정된 `granularity` 값에 따라 다릅니다. |

{style=&quot;table-layout:auto&quot;}

## 부록

다음 섹션에는 `/metrics` 끝점 작업에 대한 추가 정보가 포함되어 있습니다.

### 사용 가능한 지표 {#available-metrics}

다음 표는 [!DNL Observability Insights]에 의해 노출되고 [!DNL Platform] 서비스로 분류된 모든 지표를 나열합니다. 각 지표에는 설명 및 승인된 ID 쿼리 매개 변수가 포함되어 있습니다.

>[!NOTE]
>
>별도로 명시되어 있지 않는 한 나열된 모든 ID 쿼리 매개 변수는 선택 사항입니다.

#### [!DNL Data Ingestion] {#ingestion}

다음 표에서는 Adobe Experience Platform [!DNL Data Ingestion]에 대한 지표를 대략적으로 설명합니다. **bold**&#x200B;의 지표는 스트리밍 통합 지표입니다.

| 인사이트 지표 | 설명 | ID 쿼리 매개 변수 |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.new.count | 만든 총 데이터 집합 수입니다. | N/A |
| timeseries.ingestion.dataset.size | 데이터 세트 하나 또는 모든 데이터 세트에 대해 수집되는 모든 데이터의 누적 크기입니다. | 데이터 세트 ID |
| timeseries.ingestion.dataset.dailysize | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 일별로 수집되는 데이터의 크기입니다. | 데이터 세트 ID |
| timeseries.ingestion.dataset.batchfailed.count | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 실패한 일괄 처리 수입니다. | 데이터 세트 ID |
| timeseries.ingestion.dataset.batchsuccess.count | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 수집되는 일괄 처리 수입니다. | 데이터 세트 ID |
| timeseries.ingestion.dataset.recordsuccess.count | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 수집되는 레코드 수입니다. | 데이터 세트 ID |
| **timelines.data.collection.validation.total.messages.rate** | 하나의 데이터 세트 또는 모든 데이터 세트에 대한 총 메시지 수입니다. | 데이터 세트 ID |
| **timelines.data.collection.validation.valid.messages.rate** | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 유효한 총 메시지 수입니다. | 데이터 세트 ID |
| **timelines.data.collection.validation.invalid.messages.rate** | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 잘못된 메시지의 총 수입니다. | 데이터 세트 ID |
| **timelines.data.collection.validation.category.type.count** | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 잘못된 &quot;유형&quot; 메시지의 총 수입니다. | 데이터 세트 ID |
| **timelines.data.collection.validation.category.range.count** | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 잘못된 &quot;범위&quot; 메시지의 총 수입니다. | 데이터 세트 ID |
| **timelines.data.collection.validation.category.format.count** | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 잘못된 &quot;형식&quot; 메시지의 총 수입니다. | 데이터 세트 ID |
| **timelines.data.collection.validation.category.pattern.count** | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 잘못된 &quot;패턴&quot; 메시지의 총 수입니다. | 데이터 세트 ID |
| **timelines.data.collection.validation.category.presence.count** | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 잘못된 &quot;존재 여부&quot; 메시지의 총 수입니다. | 데이터 세트 ID |
| **timelines.data.collection.validation.category.enum.count** | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 잘못된 &quot;열거형&quot; 메시지의 총 수입니다. | 데이터 세트 ID |
| **timelines.data.collection.validation.category.unclassified.count** | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 잘못된 &quot;분류되지 않은&quot; 메시지의 총 수입니다. | 데이터 세트 ID |
| **timelines.data.collection.validation.category.unknown.count** | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 잘못된 &quot;알 수 없음&quot; 메시지의 총 수입니다. | 데이터 세트 ID |
| **timeselines.data.collection.inlet.total.messages.received** | 하나의 데이터 입력 또는 모든 데이터 입력기에 대해 수신된 총 메시지 수입니다. | 입구 ID |
| **timeselines.data.collection.total.messages.size.received** | 하나의 데이터 입력 또는 모든 데이터 입력란에 대해 수신된 데이터의 총 크기입니다. | 입구 ID |
| **timelines.data.collection.inlet.success** | 하나의 데이터 입력 또는 모든 데이터 인렛에 대한 성공적인 HTTP 호출 총 수입니다. | 입구 ID |
| **timelines.data.collection.inlet.failure** | 하나의 데이터 입력 또는 모든 데이터 인렛에 대한 실패한 HTTP 호출의 총 수입니다. | 입구 ID |

{style=&quot;table-layout:auto&quot;}

#### [!DNL Identity Service] {#identity}

다음 표에서는 Adobe Experience Platform [!DNL Identity Service]에 대한 지표를 대략적으로 설명합니다.

| 인사이트 지표 | 설명 | ID 쿼리 매개 변수 |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | 데이터 세트 하나 또는 모든 데이터 세트에 대해 [!DNL Identity Service]이(가) 데이터 소스에 쓴 레코드 수입니다. | 데이터 세트 ID |
| timeseries.identity.dataset.recordfailed.count | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 [!DNL Identity Service]이(가) 실패한 레코드 수입니다. | 데이터 세트 ID |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | 네임스페이스에 대해 인제스트된 ID 레코드 수입니다. | 네임스페이스 ID(**필수**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | 네임스페이스에 의해 실패한 ID 레코드 수입니다. | 네임스페이스 ID(**필수**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | 네임스페이스에 의해 건너뛴 ID 레코드 수입니다. | 네임스페이스 ID(**필수**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | IMS 조직에 대한 ID 그래프에 저장된 고유 ID 수. | 해당 없음 |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | 네임스페이스에 대한 ID 그래프에 저장된 고유 ID 수입니다. | 네임스페이스 ID(**필수**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | IMS 조직에 대한 ID 그래프에 저장된 고유 그래프 ID 수입니다. | 해당 없음 |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | IMS에 대한 ID 그래프에 저장된 고유 ID 수 특정 그래프 강도(&quot;알 수 없음&quot;, &quot;약함&quot; 또는 &quot;강함&quot;)에 대한 조직 | 그래프 강도(**필수**) |

{style=&quot;table-layout:auto&quot;}

#### [!DNL Privacy Service] {#privacy}

다음 표에서는 Adobe Experience Platform [!DNL Privacy Service]에 대한 지표를 대략적으로 설명합니다.

| 인사이트 지표 | 설명 | ID 쿼리 매개 변수 |
| ---- | ---- | ---- |
| timeseries.gdpr.jobs.totaljobs.count | GDPR에서 만든 총 작업 수입니다. | ENV(**필수**) |
| timeseries.gdpr.jobs.completedjobs.count | GDPR에서 완료된 총 작업 수입니다. | ENV(**필수**) |
| timeseries.gdpr.jobs.errorjobs.count | GDPR의 총 오류 작업 수입니다. | ENV(**필수**) |

{style=&quot;table-layout:auto&quot;}

#### [!DNL Query Service] {#query}

다음 표에서는 Adobe Experience Platform [!DNL Query Service]에 대한 지표를 대략적으로 설명합니다.

| 인사이트 지표 | 설명 | ID 쿼리 매개 변수 |
| ---- | ---- | ---- |
| timeseries.queryservice.query.scheduleonce.count | 반복되지 않는 총 예약 쿼리 수입니다. | 해당 없음 |
| timeseries.queryservice.query.scheduledrecurring.count | 반복 예약된 총 쿼리 수입니다. | 해당 없음 |
| timeseries.queryservice.query.batchquery.count | 실행된 일괄 처리 쿼리의 총 수입니다. | 해당 없음 |
| timeseries.queryservice.query.scheduledquery.count | 실행된 총 예약된 쿼리 수입니다. | 해당 없음 |
| timeseries.queryservice.query.interactivequery.count | 실행된 총 대화형 쿼리 수입니다. | 해당 없음 |
| timeseries.queryservice.query.batchfrompsqlquery.count | PSQL에서 실행된 총 일괄 처리 쿼리 수입니다. | 해당 없음 |

{style=&quot;table-layout:auto&quot;}

#### [!DNL Real-time Customer Profile] {#profile}

다음 표에서는 [!DNL Real-time Customer Profile]에 대한 지표를 대략적으로 설명합니다.

| 인사이트 지표 | 설명 | ID 쿼리 매개 변수 |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 [!DNL Data Lake]이(가) [!DNL Profile]에서 읽은 레코드 수입니다. | 데이터 세트 ID |
| timeseries.profiles.dataset.recordsuccess.count | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 데이터 소스에 [!DNL Profile]까지 기록된 레코드 수입니다. | 데이터 세트 ID |
| timeseries.profiles.dataset.recordfailed.count | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 [!DNL Profile]이(가) 실패한 레코드 수입니다. | 데이터 세트 ID |
| timeseries.profiles.dataset.batchsuccess.count | 데이터 세트 또는 모든 데이터 세트에 대해 수집되는 [!DNL Profile] 일괄 처리 수입니다. | 데이터 세트 ID |
| timeseries.profiles.dataset.batchfailed.count | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 [!DNL Profile] 일괄 처리 수가 실패했습니다. | 데이터 세트 ID |
| platform.ups.ingest.streaming.request.m1_rate | 들어오는 요청 비율입니다. | IMS 조직(**필수**) |
| platform.ups.ingest.streaming.access.put.success.m1_rate | 통합 성공률. | IMS 조직(**필수**) |
| platform.ups.ingest.streaming.records.created.m15_rate | 데이터 세트에 대해 수집되는 새 레코드 비율입니다. | 데이터 집합 ID(**필수**) |
| platform.ups.ingest.streaming.request.error.created.outOfOrder.m1_rate | 데이터 세트에 대한 만들기 요청을 위해 타임스탬프가 지정된 레코드 중 순서가 잘못된 레코드 비율입니다. | 데이터 집합 ID(**필수**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.created.timestamp | 데이터 세트에 대한 레코드 요청의 마지막 만들기 타임스탬프 | 데이터 집합 ID(**필수**) |
| platform.ups.ingest.streaming.request.error.updated.outOfOrder.m1_rate | 데이터 세트에 대한 업데이트 요청에 대해 순서가 잘못된 레코드 비율입니다. | 데이터 집합 ID(**필수**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.updated.timestamp | 데이터 세트에 대한 마지막 업데이트 레코드 요청에 대한 타임스탬프 | 데이터 집합 ID(**필수**) |
| platform.ups.ingest.streaming.record.size.m1_rate | 평균 레코드 크기. | IMS 조직(**필수**) |
| platform.ups.ingest.streaming.records.updated.m15_rate | 데이터 세트에 대해 수집되는 레코드에 대한 업데이트 요청 비율입니다. | 데이터 집합 ID(**필수**) |

{style=&quot;table-layout:auto&quot;}

### 오류 메시지

`/metrics` 끝점의 응답은 특정 조건에서 오류 메시지를 반환할 수 있습니다. 이러한 오류 메시지는 다음 형식으로 반환됩니다.

```json
{
    "type": "http://ns.adobe.com/aep/errors/INSGHT-1000-400",
    "title": "Bad Request - Start date cannot be after end date.",
    "status": 400,
    "report": {
        "tenantInfo": {
            "sandboxName": "prod",
            "sandboxId": "49f58060-5d47-34rd-aawf-a5384333ff12",
            "imsOrgId": "{IMS_ORG}"
        },
        "additionalContext": null
    },
    "error-chain": [
        {
            "serviceId": "INSGHT",
            "errorCode": "INSGHT-1000-400",
            "invokingServiceId": "INSGHT",
            "unixTimeStampMs": 1602095177129
        }
    ]
}
```

| 속성 | 설명 |
| --- | --- |
| `title` | 오류 메시지와 발생 가능한 이유를 포함하는 문자열입니다. |
| `report` | 이 오류를 트리거한 작업에 사용되는 샌드박스 및 IMS 조직 등 오류에 대한 컨텍스트 정보를 포함합니다. |

{style=&quot;table-layout:auto&quot;}

다음 표에는 API에서 반환할 수 있는 다양한 오류 코드가 나열되어 있습니다.

| 오류 코드 | Title | 설명 |
| --- | --- | --- |
| `INSGHT-1000-400` | 잘못된 요청 페이로드 | 요청 페이로드에 문제가 있습니다. [위](#v2)에 표시된 대로 페이로드 형식을 정확하게 일치하는지 확인합니다. 가능한 모든 이유로 이 오류가 트리거될 수 있습니다.<ul><li>`aggregator` 같은 필수 필드가 없습니다.</li><li>잘못된 지표</li><li>요청에 잘못된 수집기가 포함되어 있습니다.</li><li>종료 날짜 이후에 시작 날짜가 발생합니다.</li></ul> |
| `INSGHT-1001-400` | 지표 쿼리 실패 | 잘못된 요청이나 쿼리 자체를 구문 분석할 수 없기 때문에 지표 데이터베이스를 쿼리하는 동안 오류가 발생했습니다. 다시 시도하기 전에 요청의 형식이 올바른지 확인하십시오. |
| `INSGHT-1001-500` | 지표 쿼리 실패 | 서버 오류로 인해 지표 데이터베이스를 쿼리하는 동안 오류가 발생했습니다. 요청을 다시 시도하십시오. 문제가 지속되면 Adobe 지원 팀에 문의하십시오. |
| `INSGHT-1002-500` | 서비스 오류 | 내부 오류로 인해 요청을 처리할 수 없습니다. 요청을 다시 시도하십시오. 문제가 지속되면 Adobe 지원 팀에 문의하십시오. |
| `INSGHT-1003-401` | 샌드박스 유효성 검사 오류 | 샌드박스 유효성 검사 오류로 인해 요청을 처리할 수 없습니다. `x-sandbox-name` 헤더에서 제공한 샌드박스 이름이 IMS 조직에 대해 활성화된 유효한 샌드박스를 나타내야 합니다. 요청을 다시 시도하십시오. |

{style=&quot;table-layout:auto&quot;}
