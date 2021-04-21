---
keywords: Experience Platform;홈;인기 항목;세그멘테이션;세그멘테이션 서비스;미리 보기;미리 보기;미리 보기 및 예측;예측 및 미리 보기;api;Segmentation;Segmentation;Service;
solution: Experience Platform
title: API 끝점 미리 보기 및 예측
topic-legacy: developer guide
description: 세그먼트 정의가 개발되면 Adobe Experience Platform 내의 예측 및 미리 보기 도구를 사용하여 요약 수준 정보를 보고 예상 고객을 분리할 수 있습니다.
exl-id: 2c204f29-825f-4a5e-a7f6-40fc69263614
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 2%

---

# 끝점 미리 보기 및 예측

세그먼트 정의를 개발할 때 Adobe Experience Platform 내의 예측 및 미리 보기 도구를 사용하여 요약 수준 정보를 보고 예상하는 대상을 분리할 수 있습니다.

* **미리** 보기세그먼트 정의에 대한 페이지로 구분된 프로필 목록을 제공하므로 결과를 예상과 비교할 수 있습니다.

* **예상** 대상 크기, 신뢰 구간 및 오류 표준 편차 등 세그먼트 정의에 대한 통계 정보를 제공합니다.

>[!NOTE]
>
>특정 네임스페이스 또는 프로필 데이터 저장소의 전체 프로필 조각 및 병합된 프로필 수와 같은 실시간 고객 프로필 데이터와 관련된 비슷한 지표에 액세스하려면 프로필 API 개발자 안내서의 일부인 [프로필 미리 보기(샘플 상태 미리 보기) 끝점 안내서](../../profile/api/preview-sample-status.md)를 참조하십시오.

## 시작하기

이 안내서에 사용된 끝점은 [!DNL Adobe Experience Platform Segmentation Service] API의 일부입니다. 계속하기 전에 필수 헤더 및 예제 API 호출 방법을 포함하여 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보가 필요하면 [시작 안내서](./getting-started.md)를 검토하십시오.

## 추정치가 생성되는 방식

프로필 스토어에 레코드를 수집하면 총 프로필 수가 5% 이상 증가하거나 감소하면 샘플링 작업이 시작되어 카운트가 업데이트됩니다. 데이터 샘플링이 트리거되는 방식은 다음 섭취 방법에 따라 달라집니다.

* **일괄 처리** 처리: 배치를 성공적으로 Profile Store에 인제스트한 후 15분 이내에 5% 증가 또는 감소 임계값이 충족되면 작업을 실행하여 카운트를 업데이트합니다.
* **스트리밍 통합:** 스트리밍 데이터 워크플로우의 경우 5% 증가 또는 감소 임계값이 충족되었는지 여부를 시간별로 확인하는 검사가 수행됩니다. 있는 경우 작업이 자동으로 트리거되어 카운트가 업데이트됩니다.

스캔의 샘플 크기는 프로필 저장소의 전체 개체 수에 따라 달라집니다. 이러한 샘플 크기는 다음 표에 나와 있습니다.

| 프로필 스토어의 엔티티 | 샘플 크기 |
| ------------------------- | ----------- |
| 100만 미만 | 전체 데이터 세트 |
| 1~2,000만 | 100만 |
| 2천만 명 이상 | 합계의 5% |

>[!NOTE]
>
>추정은 일반적으로 10초에서 15초 정도 소요되며, 추정은 대략적으로 시작되며 기록을 더 많이 읽으면 세부적으로 조정됩니다.

## 새 미리 보기 {#create-preview} 만들기

`/preview` 끝점에 POST 요청을 하여 새 미리 보기를 만들 수 있습니다.

>[!NOTE]
>
>미리 보기 작업을 만들면 예측 작업이 자동으로 생성됩니다. 이 두 작업은 동일한 ID를 공유합니다.

**API 형식**

```http
POST /preview
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/preview \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
    {
        "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
        "predicateType": "pql/text",
        "predicateModel": "_xdm.context.profile"
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `predicateExpression` | 데이터를 쿼리할 PQL 표현식입니다. |
| `predicateType` | `predicateExpression` 아래의 쿼리 식에 대한 설명 유형입니다. 현재 이 속성에 대해 허용된 유일한 값은 `pql/text`입니다. |
| `predicateModel` | 프로필 데이터가 기반으로 하는 [!DNL Experience Data Model](XDM) 스키마 클래스의 이름입니다. |

**응답**

성공적인 응답은 새로 만든 미리 보기에 대한 세부 정보와 함께 HTTP 상태 201(만들어짐)을 반환합니다.

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
| `state` | 미리 보기 작업의 현재 상태입니다. 처음 만들 때 &quot;새로 만들기&quot; 상태가 됩니다. 이후 처리가 완료될 때까지 &quot;실행 중&quot; 상태가 되며, 이 시점에서 &quot;RESULT_READY&quot; 또는 &quot;FAILED&quot;가 됩니다. |
| `previewId` | 다음 섹션에 설명된 대로 예측 또는 미리 보기를 볼 때 조회 목적으로 사용할 미리 보기 작업의 ID입니다. |

## 특정 미리 보기 {#get-preview} 결과 검색

`/preview` 끝점에 GET 요청을 하고 요청 경로에 미리 보기 ID를 제공하여 특정 미리 보기에 대한 자세한 정보를 검색할 수 있습니다.

**API 형식**

```http
GET /preview/{PREVIEW_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{PREVIEW_ID}` | 검색할 미리 보기의 `previewId` 값입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 미리 보기에 대한 자세한 정보가 있는 HTTP 상태 200을 반환합니다.

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
| `results` | 관련 ID와 함께 엔티티 ID 목록입니다. 제공된 링크는 [프로필 액세스 API 끝점](../../profile/api/entities.md)을 사용하여 지정된 개체를 찾는 데 사용할 수 있습니다. |

## 특정 예상 작업 {#get-estimate} 결과 검색

미리 보기 작업을 만들었으면 `/estimate` 끝점에 대한 GET 요청 경로에 `previewId`을 사용하여 예상 대상 크기, 신뢰 구간 및 오류 표준 편차를 포함한 세그먼트 정의에 대한 통계 정보를 볼 수 있습니다.

**API 형식**

```http
GET /estimate/{PREVIEW_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{PREVIEW_ID}` | 예상 작업은 미리 보기 작업이 만들어질 때만 트리거되며, 두 작업은 조회 목적으로 동일한 ID 값을 공유합니다. 특히 미리 보기 작업을 만들 때 반환된 `previewId` 값입니다. |

**요청**

다음 요청은 특정 예상 작업의 결과를 검색합니다.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/estimate/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `estimatedNamespaceDistribution` | 세그먼트 내의 프로필 수를 ID 네임스페이스로 분류하는 개체 배열입니다. 하나의 프로필이 여러 네임스페이스와 연결될 수 있으므로 네임스페이스별 전체 프로필 수(각 네임스페이스에 대해 표시된 값을 함께 추가)는 프로필 수 지표보다 높을 수 있습니다. 예를 들어 고객이 두 개 이상의 채널에서 브랜드와 상호 작용하는 경우 여러 네임스페이스가 해당 개별 고객과 연결됩니다. |
| `state` | 미리 보기 작업의 현재 상태입니다. 처리가 완료될 때까지 상태는 &quot;RUNNING&quot;가 되며 이 시점에서 &quot;RESULT_READY&quot; 또는 &quot;FAILED&quot;가 됩니다. |
| `_links.preview` | `state`이(가) &quot;RESULT_READY&quot;인 경우 이 필드는 예상 값을 볼 수 있는 URL을 제공합니다. |

## 다음 단계

이 안내서를 읽은 후 세그멘테이션 API를 사용하여 미리 보기와 추정을 사용하는 방법을 더 잘 이해해야 합니다. 특정 네임스페이스 또는 프로필 데이터 저장소의 전체 프로필 조각 및 병합된 프로필 수와 같은 실시간 고객 프로필 데이터와 관련된 지표에 액세스하는 방법을 알아보려면 [프로필 미리 보기(`/previewsamplestatus`) 끝점 안내서](../../profile/api/preview-sample-status.md)를 방문하십시오.
