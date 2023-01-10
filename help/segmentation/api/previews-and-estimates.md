---
keywords: Experience Platform;홈;인기 항목;세그먼테이션;세그멘테이션;세그멘테이션 서비스;미리 보기;예측;미리 보기 및 예상;예측 및 미리 보기;api;API;
solution: Experience Platform
title: API 엔드포인트 미리 보기 및 예상
description: 세그먼트 정의가 개발되면 Adobe Experience Platform 내의 예측 및 미리 보기 도구를 사용하여 요약 수준 정보를 보고 예상 대상을 분리할 수 있습니다.
exl-id: 2c204f29-825f-4a5e-a7f6-40fc69263614
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 2%

---

# 미리 보기 및 예상 끝점

세그먼트 정의를 개발할 때 Adobe Experience Platform 내의 예측 및 미리 보기 도구를 사용하여 예상한 대상을 격리하는 데 도움이 되는 요약 수준 정보를 볼 수 있습니다.

* **미리 보기** 세그먼트 정의에 대해 페이지에 매겨진 자격 프로필 목록을 제공하여 결과를 예상과 비교할 수 있도록 합니다.

* **예상** 예상 대상 크기, 신뢰 구간 및 오류 표준 편차와 같은 세그먼트 정의에 대한 통계 정보를 제공합니다.

>[!NOTE]
>
>특정 네임스페이스 또는 프로필 데이터 저장소 전체에서 총 프로필 조각 및 병합된 프로필 수 등 실시간 고객 프로필 데이터와 관련된 유사한 지표에 액세스하려면 다음을 참조하십시오 [프로필 미리 보기 (샘플 상태 미리 보기) 끝점 안내서](../../profile/api/preview-sample-status.md)프로필 API 개발자 가이드의 일부입니다.

## 시작하기

이 안내서에서 사용되는 엔드포인트는 [!DNL Adobe Experience Platform Segmentation Service] API. 계속하기 전에 [시작 안내서](./getting-started.md) 필수 헤더 및 예제 API 호출을 읽는 방법을 포함하여 API를 성공적으로 호출하기 위해 알고 있어야 하는 중요한 정보입니다.

## 추정이 생성되는 방법

프로필 저장소에 레코드를 섭취할 때 총 프로필 수가 5% 이상 증가하거나 감소하면 샘플링 작업이 트리거되어 카운트가 업데이트됩니다. 데이터 샘플링을 트리거하는 방법은 수집 방법에 따라 다릅니다.

* **배치 수집:** 일괄 처리를 수집하기 위해 배치를 프로필 저장소에 성공적으로 수집한 후 15분 이내에 5% 증가 또는 감소 임계값이 충족되면 작업이 실행되어 카운트가 업데이트됩니다.
* **스트리밍 수집:** 스트리밍 데이터 워크플로우의 경우 5% 증가 또는 감소 임계값이 충족되었는지 확인하기 위해 시간별로 검사를 수행합니다. 이 경우 작업을 자동으로 트리거하여 카운트를 업데이트합니다.

검색 샘플 크기는 프로필 저장소의 전체 개체 수에 따라 다릅니다. 이러한 샘플 크기는 다음 표에 나와 있습니다.

| 프로필 저장소의 엔터티 | 샘플 크기 |
| ------------------------- | ----------- |
| 100만 미만 | 전체 데이터 세트 |
| 1~2,000만 | 100만 |
| 2천만 명 이상 | 합계의 5% |

>[!NOTE]
>
>추정은 일반적으로 실행하는 데 10~15초가 소요되며, 대략적인 추정치를 시작하고 더 많은 레코드를 읽으면 세분화됩니다.

## 새 미리 보기 만들기 {#create-preview}

에 POST 요청을 만들어 새 미리 보기를 만들 수 있습니다 `/preview` 엔드포인트.

>[!NOTE]
>
>미리 보기 작업을 만들 때 예상 작업이 자동으로 만들어집니다. 이 두 작업은 동일한 ID를 공유합니다.

**API 형식**

```http
POST /preview
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/preview \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
    {
        "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
        "predicateType": "pql/text",
        "predicateModel": "_xdm.context.profile",
        "graphType": "none"
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `predicateExpression` | 데이터를 쿼리할 PQL 표현식입니다. |
| `predicateType` | 아래의 쿼리 식에 대한 설명 유형입니다. `predicateExpression`. 현재 이 속성에 대해 허용되는 값은 `pql/text`. |
| `predicateModel` | 의 이름 [!DNL Experience Data Model] 프로필 데이터가 기반으로 하는 (XDM) 스키마 클래스입니다. |
| `graphType` | 클러스터를 가져올 그래프 유형입니다. 지원되는 값은 다음과 같습니다 `none` (ID 결합을 수행하지 않음) 및 `pdg` (개인 id 그래프를 기반으로 ID 결합을 수행합니다.) |

**응답**

성공적인 응답은 새로 만든 미리 보기에 대한 세부 정보와 함께 HTTP 상태 201(생성됨)을 반환합니다.

```json
{
    "state": "NEW",
    "previewQueryId": "e890068b-f5ca-4a8f-a6b5-af87ff0caac3",
    "previewQueryStatus": "NEW",
    "previewId": "MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow",
    "previewExecutionId": 0
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `state` | 미리 보기 작업의 현재 상태입니다. 처음 만들 때 &quot;NEW&quot; 상태가 됩니다. 그런 다음 처리가 완료될 때까지 &quot;실행 중&quot; 상태로, 이 경우 &quot;RESULT_READY&quot; 또는 &quot;FAILED&quot;가 됩니다. |
| `previewId` | 다음 섹션에 요약된 대로 예측 또는 미리 보기를 볼 때 조회 목적으로 사용할 미리 보기 작업의 ID입니다. |

## 특정 미리 보기의 결과를 검색합니다 {#get-preview}

에 GET 요청을 수행하여 특정 미리 보기에 대한 자세한 정보를 검색할 수 있습니다 `/preview` 엔드포인트 및 요청 경로에 미리 보기 ID를 제공합니다.

**API 형식**

```http
GET /preview/{PREVIEW_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{PREVIEW_ID}` | 다음 `previewId` 검색할 미리 보기 값입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 미리 보기에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
   "results": [{
        "XID_ADOBE-MARKETING-CLOUD-ID-1": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_ADOBE-MARKETING-CLOUD-ID-1",
            "endCustomerIds": {
                "XID_COOKIE_ID_1": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE_ID_1"
                },
                "XID_PROFILE_ID_1": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_PROFILE_ID_1"
                }
            }
        }
    },
    {
        "XID_COOKIE-ID-2": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE-ID-2",
            "endCustomerIds": {
                "XID_COOKIE_ID_2-1": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE_ID_2-1"

                },
                "XID_PROFILE_ID_2": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_PROFILE_ID_2"
                }
            }
        },
        "XID_ADOBE-MARKETING-CLOUD-ID-3": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_ADOBE-MARKETING-CLOUD-ID-1000"
        }
    }],
    "state": "RESULT_READY",
    "links": {
        "_self": "https://platform.adobe.io/data/core/ups/preview?expression=<expr-1>&limit=1000",
        "next": "",
        "prev": ""
    },
    "page": {
        "offset": 0,
        "size": 3
    }
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `results` | 관련 ID와 함께 엔티티 ID 목록입니다. 제공된 링크를 사용하여 [프로필 액세스 API 끝점](../../profile/api/entities.md). |

## 특정 예상 작업의 결과 검색 {#get-estimate}

미리 보기 작업을 만들면 이 작업을 사용할 수 있습니다 `previewId` 에 대한 GET 요청 경로 `/estimate` 예상 대상 크기, 신뢰 구간 및 오류 표준 편차를 포함하여 세그먼트 정의에 대한 통계 정보를 보는 끝점입니다.

**API 형식**

```http
GET /estimate/{PREVIEW_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{PREVIEW_ID}` | 예상 작업은 미리 보기 작업을 만들 때만 트리거되며 두 작업이 조회 목적으로 동일한 ID 값을 공유합니다. 특히, 다음과 같습니다 `previewId` 미리 보기 작업을 만들 때 반환된 값입니다. |

**요청**

다음 요청은 특정 예상 작업의 결과를 검색합니다.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/estimate/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공한 응답은 예상 작업의 세부 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
    "estimatedSize": 4275,
    "numRowsToRead": 4275,
    "estimatedNamespaceDistribution": [
        {
            "namespaceId": "4",
            "profilesMatchedSoFar": 35
        },
        {
            "namespaceId": "6",
            "profilesMatchedSoFar": 4275
        }
    ],
    "state": "RESULT_READY",
    "profilesReadSoFar": 4275,
    "standardError": 0,
    "error": {
        "description": "",
        "traceback": ""
    },
    "profilesMatchedSoFar": 4275,
    "totalRows": 4275,
    "confidenceInterval": "95%",
    "_links": {
        "preview": "https://platform.adobe.io/data/core/ups/preview/app-32be0328-3f31-4b64-8d84-acd0c4fbdad3/execution/0?previewQueryId=e890068b-f5ca-4a8f-a6b5-af87ff0caac3"
    }
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `estimatedNamespaceDistribution` | 세그먼트 내의 프로필 수를 ID 네임스페이스로 분류하는 개체 배열입니다. 네임스페이스별 총 프로필 수(각 네임스페이스에 대해 표시된 값을 함께 추가)는 한 개의 프로필이 여러 네임스페이스와 연결될 수 있으므로 프로필 수 지표보다 높을 수 있습니다. 예를 들어 고객이 둘 이상의 채널에서 브랜드와 상호 작용하는 경우 여러 네임스페이스가 해당 개별 고객과 연결됩니다. |
| `state` | 미리 보기 작업의 현재 상태입니다. 상태는 처리가 완료될 때까지 &quot;RUNNING&quot;이며, 이 시점에서 &quot;RESULT_READY&quot; 또는 &quot;FAILED&quot;가 됩니다. |
| `_links.preview` | 이 `state` 가 &quot;RESULT_READY&quot;인 경우 이 필드는 예상 URL을 제공합니다. |

## 다음 단계

이 안내서를 읽은 후에는 세그멘테이션 API를 사용하여 미리 보기 및 예측을 사용하는 방법을 더 잘 이해할 수 있어야 합니다. 전체 프로필 조각 및 특정 네임스페이스 또는 프로필 데이터 저장소 내 병합된 프로필 수 등 실시간 고객 프로필 데이터와 관련된 지표에 액세스하는 방법을 알려면 다음을 방문하십시오. [프로필 미리 보기 (`/previewsamplestatus`) endpoint 안내서](../../profile/api/preview-sample-status.md).
