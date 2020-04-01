---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform 통찰력 통찰력
topic: overview
translation-type: tm+mt
source-git-commit: 947955403a270914437d9172bca458f9c49ccd8f

---


# Adobe Experience Platform 통찰력 인사이트 개요

Observability Insights는 Adobe Experience Platform에서 주요 관측 가능성 지표를 노출할 수 있는 RESTful API입니다. 이러한 지표는 플랫폼 사용 통계, 플랫폼 서비스 상태 점검, 이전 동향 및 다양한 플랫폼 기능에 대한 성능 지표에 대한 통찰력을 제공합니다.

이 문서에서는 Observability Insights API에 대한 예제 호출을 시연하고 서비스와 호환되는 노출된 지표 목록을 제공합니다. 관찰 가능한 끝점의 전체 목록은 Observability Insights [API 참조를](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml)참조하십시오.

## 시작하기

플랫폼 API를 호출하려면 먼저 [인증 자습서를](../tutorials/authentication.md)완료해야 합니다. 인증 튜토리얼을 완료하면 다음과 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값이 제공됩니다.

* 인증:베어러 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

경험 플랫폼의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. 플랫폼 API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 플랫폼의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서를](../sandboxes/home.md)참조하십시오.

## 관찰 가능한 지표 검색

Observability Insights API에서 `/metrics` 종단점에 GET 요청을 작성하여 관찰 가능한 지표를 검색할 수 있습니다.

**API 형식**

끝점을 사용할 때 `/metrics` 하나 이상의 지표 요청 매개 변수를 제공해야 합니다. 다른 쿼리 매개 변수는 결과 필터링을 위해 선택 사항입니다.

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
| `{ID}` | 지표를 노출하려는 특정 플랫폼 리소스의 식별자입니다. 이 ID는 사용 중인 지표에 따라 선택 사항이거나 필수 사항이거나 해당되지 않을 수 있습니다. 각 지표에 대해 지원되는 ID(필수 및 선택 사항 모두)와 사용 가능한 지표 목록은 아래 [사용 가능한 지표에](metrics.md) 대한 참조 문서를 참조하십시오. |
| `{DATE_RANGE}` | 노출할 지표의 날짜 범위(예: ISO 8601 형식)입니다 `2018-10-01T07:00:00.000Z/2018-10-09T07:00:00.000Z`. |

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

성공적인 응답은 제공된 시간 `dateRange` 및 요청 경로에 지정된 지표에 대한 해당 값을 포함하는 개체 목록을 반환합니다. 플랫폼 리소스의 `id` 사용이 요청 경로에 포함되는 경우 결과는 해당 특정 리소스에만 적용됩니다. 를 생략하면 `id` IMS 조직 내에서 적용 가능한 모든 리소스에 결과가 적용됩니다.

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

## 다음 단계

이 문서에서는 Observability Insights API에 대한 개요를 제공합니다. API에서 사용할 수 있는 지표의 전체 목록을 보려면 [사용 가능한 지표에](metrics.md) 대한 문서를 참조하십시오.