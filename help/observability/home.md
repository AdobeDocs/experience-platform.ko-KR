---
keywords: Experience Platform;home;popular topics;date range
solution: Experience Platform
title: Adobe Experience Platform 통찰력 통찰력
topic: overview
description: Observability Insights는 Adobe Experience Platform에서 주요 관측 가능 지표를 노출할 수 있는 RESTful API입니다. 이러한 지표는 플랫폼 사용 통계, 플랫폼 서비스 상태 점검, 이전 동향 및 다양한 플랫폼 기능에 대한 성능 지표에 대한 통찰력을 제공합니다.
translation-type: tm+mt
source-git-commit: cc81d590f308c7e2677cec000c27e8aca42437f5
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 2%

---


# Adobe Experience Platform 통찰력 통찰력 개요

Observability Insights는 Adobe Experience Platform에서 주요 관측 가능 지표를 노출할 수 있는 RESTful API입니다. 이러한 지표는 다양한 기능에 대한 [!DNL Platform] 사용 통계, 서비스 상태 점검, [!DNL Platform] 내역 동향 및 성과 지표에 대한 통찰력을 [!DNL Platform] 제공합니다.

이 문서에서는 Observability Insights API에 대한 예제 호출을 보여 줍니다. 관측 가능한 끝점의 전체 목록은 Observability Insights [API 참조를 참조하십시오](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml).

## 시작하기

API를 호출하려면 [!DNL Platform] 먼저 [인증 자습서를 완료해야 합니다](../tutorials/authentication.md). 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* 인증:무기명 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

의 모든 리소스 [!DNL Experience Platform] 는 특정 가상 샌드박스와 분리됩니다. API에 대한 모든 [!DNL Platform] 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다. 의 샌드박스에 대한 자세한 내용 [!DNL Platform]은 [샌드박스 개요 설명서를 참조하십시오](../sandboxes/home.md).

* x-sandbox-name: `{SANDBOX_NAME}`

## 관측 가능한 지표 검색

Observability Insights API에서 종단점에 대한 GET 요청을 수행하여 관측 가능한 지표를 검색할 수 `/metrics` 있습니다.

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
| `{ID}` | 지표를 노출하려는 특정 [!DNL Platform] 리소스의 식별자입니다. 이 ID는 사용 중인 지표에 따라 선택 사항이거나 필수 또는 적용되지 않을 수 있습니다. 각 지표에 대해 지원되는 ID(필수 및 선택 사항 모두)와 함께 사용 가능한 지표 목록을 보려면 [사용 가능한 지표에 대한 참조 문서를 참조하십시오](metrics.md). |
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

## 다음 단계

이 문서에서는 Observability Insights API에 대한 개요를 제공합니다. API에서 사용할 수 있는 전체 지표 [](metrics.md) 목록은 사용 가능한 지표에 대한 문서를 참조하십시오.