---
keywords: Experience Platform;홈;인기 항목;세그먼테이션;세그먼테이션;세그먼테이션 서비스;미리 보기;예상;미리 보기 및 예상;예상 및 미리 보기;API;API;
solution: Experience Platform
title: API 끝점 미리 보기 및 예상
description: 세그먼트 정의가 개발되면 Adobe Experience Platform 내의 예상 및 미리 보기 도구를 사용하여 요약 수준 정보를 보고 예상 대상을 격리할 수 있습니다.
exl-id: 2c204f29-825f-4a5e-a7f6-40fc69263614
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 2%

---

# 엔드포인트 미리 보기 및 예측

세그먼트 정의를 개발할 때, Adobe Experience Platform 내의 예상 및 미리 보기 도구를 사용하여 요약 수준 정보를 볼 수 있으므로 예상한 대상자를 격리하는 데 도움이 됩니다.

* **미리 보기** 세그먼트 정의에 대해 자격이 있는 프로필의 페이지가 매겨진 목록을 제공하여 예상한 결과와 비교할 수 있도록 합니다.

* **예상** 예상 대상 크기, 신뢰 구간 및 오류 표준 편차와 같은 세그먼트 정의에 대한 통계 정보를 제공합니다.

>[!NOTE]
>
>특정 네임스페이스 또는 프로필 데이터 저장소 전체에서 프로필 조각 및 병합된 프로필의 총 수와 같은 실시간 고객 프로필 데이터와 관련된 유사한 지표에 액세스하려면 다음을 참조하십시오. [프로필 미리보기(미리보기 샘플 상태) endpoint guide](../../profile/api/preview-sample-status.md): 프로필 API 개발자 안내서의 일부입니다.

## 시작하기

이 안내서에 사용된 끝점은 [!DNL Adobe Experience Platform Segmentation Service] API. 계속하기 전에 다음을 검토하십시오. [시작 안내서](./getting-started.md) 필수 헤더와 예제 API 호출을 읽는 방법 등 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보입니다.

## 예상 생성 방법

프로필 스토어로 레코드를 수집하면 총 프로필 수가 5% 이상 증가하거나 감소하면 샘플링 작업이 트리거되어 수를 업데이트합니다. 데이터 샘플링이 트리거되는 방식은 수집 방법에 따라 다릅니다.

* **일괄 처리 수집:** 일괄 처리 수집의 경우, 프로필 스토어에 일괄 처리를 성공적으로 수집한 후 15분 이내에 5% 증가 또는 감소 임계값이 충족되면 카운트를 업데이트하는 작업이 실행됩니다.
* **스트리밍 수집:** 스트리밍 데이터 워크플로의 경우 5% 증가 또는 감소 임계값이 충족되었는지 확인하기 위해 시간별로 검사가 수행됩니다. 이 경우 카운트를 업데이트하기 위해 작업이 자동으로 트리거됩니다.

스캔의 샘플 크기는 프로필 스토어에 있는 전체 엔티티 수에 따라 다릅니다. 이러한 샘플 크기는 다음 표에 나와 있습니다.

| 프로필 저장소의 엔티티 | 샘플 크기 |
| ------------------------- | ----------- |
| 100만 미만 | 전체 데이터 세트 |
| 1000~2000만 | 100만 |
| 2,000만 이상 | 총 5% |

>[!NOTE]
>
>예측은 일반적으로 10~15초 정도 소요되며, 대략적인 예측부터 시작하여 더 많은 기록을 읽을수록 수정됩니다.

## 새 미리보기 만들기 {#create-preview}

에 POST 요청을 하여 새 미리보기를 만들 수 있습니다. `/preview` 엔드포인트.

>[!NOTE]
>
>미리보기 작업이 생성되면 예측 작업이 자동으로 생성됩니다. 이 두 작업은 동일한 ID를 공유합니다.

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
| `predicateExpression` | 데이터를 쿼리할 PQL 표현식. |
| `predicateType` | 다음 구문을 사용하는 쿼리 식의 조건자 유형 `predicateExpression`. 현재 이 속성에 대해 허용되는 유일한 값은 입니다. `pql/text`. |
| `predicateModel` | 의 이름입니다. [!DNL Experience Data Model] 프로필 데이터의 기반이 되는 (XDM) 스키마 클래스. |
| `graphType` | 클러스터를 가져올 그래프 유형입니다. 지원되는 값은 다음과 같습니다 `none` (id 결합을 수행하지 않음) 및 `pdg` (개인 id 그래프를 기반으로 id 결합을 수행합니다.) |

**응답**

성공한 응답은 새로 만든 미리보기에 대한 세부 정보와 함께 HTTP 상태 201(생성됨)을 반환합니다.

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
| `state` | 미리보기 작업의 현재 상태입니다. 처음 생성될 때 &quot;NEW&quot; 상태가 됩니다. 그런 다음 처리가 완료될 때까지 &quot;RUNNING&quot; 상태가 되고 이 시점에서 &quot;RESULT_READY&quot; 또는 &quot;FAILED&quot;가 됩니다. |
| `previewId` | 다음 섹션에 설명된 대로 예상 또는 미리보기를 볼 때 조회 목적으로 사용되는 미리보기 작업의 ID입니다. |

## 특정 미리보기 결과 검색 {#get-preview}

에 GET 요청을 하여 특정 미리보기에 대한 자세한 정보를 검색할 수 있습니다. `/preview` 엔드포인트 및 요청 경로에 미리보기 ID 제공

**API 형식**

```http
GET /preview/{PREVIEW_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{PREVIEW_ID}` | 다음 `previewId` 검색할 미리보기 값. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공한 응답은 지정된 미리 보기에 대한 자세한 정보와 함께 HTTP 상태 200을 반환합니다.

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
| `results` | 관련 ID와 함께 엔티티 ID 목록입니다. 제공된 링크는 를 사용하여 지정된 엔티티를 조회하는 데 사용할 수 있습니다 [프로필 액세스 API 엔드포인트](../../profile/api/entities.md). |

## 특정 예상 작업의 결과 검색 {#get-estimate}

미리보기 작업을 생성했으면 미리보기 작업을 사용할 수 있습니다 `previewId` 에 대한 GET 요청 경로 `/estimate` 예상 대상 크기, 신뢰 구간 및 오류 표준 편차를 포함하여 세그먼트 정의에 대한 통계 정보를 보기 위한 끝점입니다.

**API 형식**

```http
GET /estimate/{PREVIEW_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{PREVIEW_ID}` | 예상 작업은 미리 보기 작업이 만들어지고 두 작업이 조회 목적으로 동일한 ID 값을 공유하는 경우에만 트리거됩니다. 특히 다음과 같습니다 `previewId` 미리보기 작업이 생성될 때 값이 반환되었습니다. |

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

성공적인 응답은 예상 작업의 세부 정보와 함께 HTTP 상태 200을 반환합니다.

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
| `estimatedNamespaceDistribution` | 세그먼트 내의 프로필 수를 ID 네임스페이스별로 분류한 오브젝트 배열입니다. 하나의 프로필이 여러 네임스페이스와 연결될 수 있으므로 네임스페이스별 총 프로필 수(각 네임스페이스에 대해 표시된 값을 함께 추가)는 프로필 수 지표보다 높을 수 있습니다. 예를 들어 고객이 둘 이상의 채널에서 브랜드와 상호 작용하는 경우 여러 네임스페이스가 해당 개별 고객과 연결됩니다. |
| `state` | 미리보기 작업의 현재 상태입니다. 처리가 완료될 때까지 상태는 &quot;RUNNING&quot;이 되며, 이 시점에서 상태는 &quot;RESULT_READY&quot; 또는 &quot;FAILED&quot;가 됩니다. |
| `_links.preview` | 다음의 경우 `state` 는 &quot;RESULT_READY&quot;이며 이 필드는 예상치를 볼 수 있는 URL을 제공합니다. |

## 다음 단계

이 안내서를 읽은 후에는 Segmentation API를 사용하여 미리보기 및 예상 값을 사용하는 방법을 더 잘 이해할 수 있습니다. 특정 네임스페이스 또는 프로필 데이터 저장소 전체에서 프로필 조각 및 병합된 프로필의 총 수와 같은 실시간 고객 프로필 데이터와 관련된 지표에 액세스하는 방법을 알아보려면 다음을 방문하십시오. [프로필 미리 보기(`/previewsamplestatus`) 엔드포인트 가이드](../../profile/api/preview-sample-status.md).
