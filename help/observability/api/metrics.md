---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 사용 가능한 지표
topic: developer guide
translation-type: tm+mt
source-git-commit: c5455dc0812b251483170ac19506d7c60ad4ecaa
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 2%

---


# 지표 끝점

관찰 가능한 지표는 Adobe Experience Platform의 다양한 기능에 대한 사용 통계, 내역 트렌드 및 성과 지표에 대한 통찰력을 제공합니다. 의 `/metrics` 종점을 [!DNL Observability Insights API] 사용하면 조직의 활동에 대한 지표 데이터를 프로그래밍 방식으로 검색할 수 있습니다 [!DNL Platform].

## 시작하기

이 안내서에서 사용되는 API 끝점은 [[!DNL Observability Insights] API의 일부입니다](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml). 계속하기 전에 [시작하기 가이드](./getting-started.md) 에서 관련 문서 링크, 이 문서에서 샘플 API 호출 읽기 안내서, 모든 API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 검토하십시오 [!DNL Experience Platform] .

## 관측 가능한 지표 검색

API의 종단점에 GET 요청을 함으로써 관측 가능한 지표를 검색할 수 `/metrics` [!DNL Observability Insights] 있습니다.

**API 형식**

끝점을 사용할 때 `/metrics` 지표 요청 매개 변수를 하나 이상 제공해야 합니다. 다른 쿼리 매개 변수는 결과 필터링을 위해 선택 사항입니다.

```http
GET /metrics?metric={METRIC}
GET /metrics?metric={METRIC}&metric={METRIC_2}
GET /metrics?metric={METRIC}&id={ID}
GET /metrics?metric={METRIC}&dateRange={DATE_RANGE}
GET /metrics?metric={METRIC}&metric={METRIC_2}&id={ID}&dateRange={DATE_RANGE}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{METRIC}` | 노출할 지표. 단일 호출에서 여러 지표를 결합할 때는 앰퍼샌드(`&`)를 사용하여 개별 지표를 구분해야 합니다. 예, `metric={METRIC_1}&metric={METRIC_2}`. |
| `{ID}` | 지표를 노출하려는 특정 [!DNL Platform] 리소스의 식별자입니다. 이 ID는 사용 중인 지표에 따라 선택 사항이거나 필수 또는 적용되지 않을 수 있습니다. 사용 가능한 지표 목록과 각 지표에 대해 지원되는 ID(필수 및 선택 사항 모두)는 [부록을](#available-metrics) 참조하십시오. |
| `{DATE_RANGE}` | 노출할 지표에 대한 날짜 범위(예: ISO 8601 형식) `2018-10-01T07:00:00.000Z/2018-10-09T07:00:00.000Z`. |

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

성공적인 응답으로 제공된 경로 내의 타임스탬프와 요청 경로에 지정된 지표에 대한 해당 값이 각각 들어 있는 객체 목록 `dateRange` 을 반환합니다. 요청 경로 `id` 에 [!DNL Platform] 리소스의 값이 포함된 경우 결과는 해당 특정 리소스에만 적용됩니다. 이 `id` 를 생략하면 IMS 조직 내의 해당 모든 리소스에 결과가 적용됩니다.

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

## 부록

다음 섹션에는 종단점 작업에 대한 추가 정보가 `/metrics` 포함되어 있습니다.

### 사용 가능한 지표 {#available-metrics}

다음 표에는 서비스에 의해 분류된 모든 지표 [!DNL Observability Insights]가 [!DNL Platform] 나열됩니다. 각 지표에는 설명 및 승인된 ID 쿼리 매개 변수가 포함됩니다.

>[!NOTE]
>
>별도로 명시하지 않는 한 나열된 모든 ID 쿼리 매개 변수는 선택 사항입니다.

#### [!DNL Data Ingestion] {#ingestion}

다음 표에서는 Adobe Experience Platform에 대한 지표에 대해 간략히 설명합니다 [!DNL Data Ingestion]. 굵게 표시된 **** 지표는 스트리밍 통합 지표입니다.

| 인사이트 지표 | 설명 | ID 쿼리 매개 변수 |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.new.count | 생성된 총 데이터 집합 수입니다. | N/A |
| timeseries.ingestion.dataset.size | 데이터 세트 하나 또는 모든 데이터 세트에 대해 수집되는 모든 데이터의 누적 크기 | 데이터 집합 ID |
| timeseries.ingestion.dataset.dailysize | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 일별로 수집되는 데이터의 크기입니다. | 데이터 집합 ID |
| timeseries.ingestion.dataset.batchfailed.count | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 실패한 일괄 처리 수입니다. | 데이터 집합 ID |
| timeseries.ingestion.dataset.batchsuccess.count | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 수집되는 일괄 처리 수입니다. | 데이터 집합 ID |
| timeseries.ingestion.dataset.recordsuccess.count | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 수집되는 레코드 수입니다. | 데이터 집합 ID |
| **timeselines.data.collection.validation.total.messages.rate** | 하나의 데이터 세트 또는 모든 데이터 세트에 대한 총 메시지 수입니다. | 데이터 집합 ID |
| **timeselines.data.collection.validation.valid.messages.rate** | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 유효한 총 메시지 수입니다. | 데이터 집합 ID |
| **timeselines.data.collection.validation.invalid.messages.rate** | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 잘못된 메시지의 총 수입니다. | 데이터 집합 ID |
| **timeselines.data.collection.validation.category.type.count** | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 잘못된 &quot;유형&quot; 메시지의 총 수입니다. | 데이터 집합 ID |
| **timeselines.data.collection.validation.category.range.count** | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 잘못된 &quot;범위&quot; 메시지의 총 수입니다. | 데이터 집합 ID |
| **timeselines.data.collection.validation.category.format.count** | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 잘못된 &quot;형식&quot; 메시지의 총 수입니다. | 데이터 집합 ID |
| **timeselines.data.collection.validation.category.pattern.count** | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 잘못된 &quot;패턴&quot; 메시지의 총 수입니다. | 데이터 집합 ID |
| **timeselines.data.collection.validation.category.presence.count** | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 잘못된 &quot;존재&quot; 메시지의 총 수입니다. | 데이터 집합 ID |
| **timeselines.data.collection.validation.category.enum.count** | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 잘못된 &quot;열거형&quot; 메시지의 총 수입니다. | 데이터 집합 ID |
| **timelines.data.collection.validation.category.unclassified.count** | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 잘못된 &quot;분류되지 않은&quot; 메시지의 총 수입니다. | 데이터 집합 ID |
| **timeselines.data.collection.validation.category.unknown.count** | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 잘못된 &quot;알 수 없음&quot; 메시지의 총 수입니다. | 데이터 집합 ID |
| **timeselines.data.collection.total.messages.received** | 하나의 데이터 입력 또는 모든 데이터 입력에 대해 수신된 메시지의 총 수입니다. | 입구 ID |
| **timeselines.data.collection.total.messages.size.received** | 하나의 데이터 입력 또는 모든 데이터 입력란에 대해 수신된 데이터의 총 크기입니다. | 입구 ID |
| **timesels.data.collection.inlet.success** | 하나의 데이터 입력부 또는 모든 데이터 입력란에 대한 성공적인 HTTP 호출의 총 수입니다. | 입구 ID |
| **timeselines.data.collection.inlet.failure** | 하나의 데이터 입력부 또는 모든 데이터 입력에 대한 실패한 HTTP 호출의 총 수입니다. | 입구 ID |

#### [!DNL Identity Service] {#identity}

다음 표에서는 Adobe Experience Platform에 대한 지표에 대해 간략히 설명합니다 [!DNL Identity Service].

| 인사이트 지표 | 설명 | ID 쿼리 매개 변수 |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 데이터 소스 [!DNL Identity Service]에 기록된 레코드 수입니다. | 데이터 집합 ID |
| timeseries.identity.dataset.recordfailed.count | 한 데이터 세트 [!DNL Identity Service]또는 모든 데이터 세트에 대해 실패한 레코드 수입니다. | 데이터 집합 ID |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | 네임스페이스에 대해 수집된 ID 레코드 수입니다. | 네임스페이스 ID(**필수**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | 네임스페이스에 의해 실패한 ID 레코드 수입니다. | 네임스페이스 ID(**필수**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | 네임스페이스가 건너뛴 ID 레코드 수입니다. | 네임스페이스 ID(**필수**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | IMS 조직의 ID 그래프에 저장된 고유 ID 수. | N/A |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | 네임스페이스에 대한 ID 그래프에 저장된 고유 ID의 수입니다. | 네임스페이스 ID(**필수**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | IMS 조직의 ID 그래프에 저장된 고유한 그래프 ID의 수입니다. | N/A |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | IMS 조직에 대해 ID 그래프에 저장된 고유 ID 수(&quot;알 수 없음&quot;, &quot;약함&quot; 또는 &quot;강함&quot;). | 그래프 강도(**필수**) |

#### [!DNL Privacy Service] {#privacy}

다음 표에서는 Adobe Experience Platform에 대한 지표에 대해 간략히 설명합니다 [!DNL Privacy Service].

| 인사이트 지표 | 설명 | ID 쿼리 매개 변수 |
| ---- | ---- | ---- |
| timeseries.gdpr.jobs.totaljobs.count | GDPR에서 만든 총 작업 수입니다. | ENV(**필수**) |
| timeseries.gdpr.jobs.completedjobs.count | GDPR에서 완료된 총 작업 수입니다. | ENV(**필수**) |
| timeseries.gdpr.jobs.errorjobs.count | GDPR의 총 오류 작업 수입니다. | ENV(**필수**) |

#### [!DNL Query Service] {#query}

다음 표에서는 Adobe Experience Platform에 대한 지표에 대해 간략히 설명합니다 [!DNL Query Service].

| 인사이트 지표 | 설명 | ID 쿼리 매개 변수 |
| ---- | ---- | ---- |
| timeseries.queryservice.query.scheduleonce.count | 반복되지 않는 예약된 쿼리의 총 수입니다. | N/A |
| timeseries.queryservice.query.scheduledrecurring.count | 예약된 총 쿼리 수입니다. | N/A |
| timeseries.queryservice.query.batchquery.count | 실행된 일괄 처리 쿼리의 총 수입니다. | N/A |
| timeseries.queryservice.query.scheduledquery.count | 실행된 예약 쿼리의 총 수입니다. | N/A |
| timeseries.queryservice.query.interactivequery.count | 실행된 대화형 쿼리의 총 수입니다. | N/A |
| timeseries.queryservice.query.batchfrompsqlquery.count | PSQL에서 실행된 일괄 처리 쿼리의 총 수입니다. | N/A |

#### [!DNL Real-time Customer Profile] {#profile}

다음 표에서는 에 대한 지표에 대해 대략적으로 설명합니다 [!DNL Real-time Customer Profile].

| 인사이트 지표 | 설명 | ID 쿼리 매개 변수 |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 [!DNL Data Lake] 에서 [!DNL Profile]읽은 레코드 수입니다. | 데이터 집합 ID |
| timeseries.profiles.dataset.recordsuccess.count | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 데이터 소스 [!DNL Profile]에 기록하는 레코드 수입니다. | 데이터 집합 ID |
| timeseries.profiles.dataset.recordfailed.count | 한 데이터 세트 [!DNL Profile]또는 모든 데이터 세트에 대해 실패한 레코드 수입니다. | 데이터 집합 ID |
| timeseries.profiles.dataset.batchsuccess.count | 데이터 세트 또는 모든 데이터 세트에 대해 수집되는 [!DNL Profile] 일괄 처리 수입니다. | 데이터 집합 ID |
| timeseries.profiles.dataset.batchfailed.count | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 실패한 [!DNL Profile] 일괄 처리 수입니다. | 데이터 집합 ID |
| platform.ups.ingest.streaming.request.m1_rate | 수신 요청 비율입니다. | IMS 조직(**필수**) |
| platform.ups.ingest.streaming.access.put.success.m1_rate | 통합 성공률 | IMS 조직(**필수**) |
| platform.ups.ingest.streaming.records.created.m15_rate | 데이터 세트에 대해 수집되는 새 레코드 비율입니다. | 데이터 집합 ID(**필수**) |
| platform.ups.ingest.streaming.request.error.created.outOfOrder.m1_rate | 데이터 세트에 대한 만들기 요청에 대해 순서가 맞지 않은 타임스탬프 레코드의 비율입니다. | 데이터 집합 ID(**필수**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.created.timestamp | 데이터 세트에 대한 마지막으로 레코드 요청을 만드는 타임스탬프 | 데이터 집합 ID(**필수**) |
| platform.ups.ingest.streaming.request.error.updated.outOfOrder.m1_rate | 데이터 세트에 대한 업데이트 요청에 대해 순서가 맞지 않은 타임스탬프가 지정된 레코드 비율입니다. | 데이터 집합 ID(**필수**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.updated.timestamp | 데이터 세트에 대한 마지막 업데이트 레코드 요청에 대한 타임스탬프 | 데이터 집합 ID(**필수**) |
| platform.ups.ingest.streaming.record.size.m1_rate | 평균 레코드 크기. | IMS 조직(**필수**) |
| platform.ups.ingest.streaming.records.updated.m15_rate | 데이터 세트에 대해 수집되는 레코드에 대한 업데이트 요청 비율입니다. | 데이터 집합 ID(**필수**) |