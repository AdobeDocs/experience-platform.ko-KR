---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;previews;estimates;previews and estimates;estimates and previews;api;API;
solution: Experience Platform
title: 끝점 미리 보기 및 예측
topic: developer guide
description: 세그먼트 정의를 개발할 때 Adobe Experience Platform 내의 예측 및 미리 보기 도구를 사용하여 요약 수준 정보를 보고 예상 고객을 분리할 수 있습니다.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 2%

---


# 끝점 미리 보기 및 예측

세그먼트 정의를 개발하면 내 [!DNL Adobe Experience Platform] 에서 예측 및 미리 보기 도구를 사용하여 예상 대상을 분리하는 데 도움이 되는 요약 수준 정보를 볼 수 있습니다. **미리** 보기에서는 세그먼트 정의에 대해 페이지에 지정된 프로필 목록을 제공하므로 결과를 예상과 비교할 수 있습니다. **예상 대상 크기, 신뢰 구간 및 오류 표준 편차와 같은 세그먼트 정의에 대한 통계 정보를 제공합니다** .

## 시작하기

이 안내서에 사용되는 끝점은 [!DNL Adobe Experience Platform Segmentation Service] API의 일부입니다. 계속하기 전에 [시작 안내서](./getting-started.md) 에서 필수 머리글 및 예제 API 호출 읽기 방법을 포함하여 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보를 검토하십시오.

## 예상 생성 방법

데이터 샘플링이 트리거되는 방법은 섭취 방법에 따라 다릅니다.

일괄 처리를 위해 프로필 스토어는 마지막 샘플링 작업이 실행된 이후 새 일괄 처리가 성공적으로 수집되었는지 확인하기 위해 15분마다 자동으로 스캔됩니다. 그런 경우 프로필 스토어는 이후 스캔되어 레코드 수가 5% 이상 변경되었는지 확인합니다. 이러한 조건이 충족되면 새 샘플링 작업이 트리거됩니다.

스트리밍 통합 시, 프로필 스토어는 매시간마다 자동으로 스캔되어 레코드 수가 최소 5% 이상 변경되었는지 확인합니다. 이 조건이 충족되면 새 샘플링 작업이 트리거됩니다.

스캔 샘플 크기는 프로필 스토어의 전체 개체 수에 따라 달라집니다. 이러한 샘플 크기는 다음 표에 나와 있습니다.

| 프로필 스토어의 엔티티 | 샘플 크기 |
| ------------------------- | ----------- |
| 100만 미만 | 전체 데이터 세트 |
| 1~2000만 | 100만 |
| 2,000만 이상 | 합계의 5% |

>[!NOTE]
>
>추정은 일반적으로 10초에서 15초 정도 소요되며, 추정은 더 많은 기록을 읽으면서 세부적으로 시작합니다.

## Create a new preview {#create-preview}

종단점에 POST 요청을 만들어 새 미리 보기를 만들 수 `/preview` 있습니다.

>[!NOTE]
>
>미리 보기 작업을 만들면 예상 작업이 자동으로 생성됩니다. 이 두 작업은 동일한 ID를 공유합니다.

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
| `predicateExpression` | 데이터를 쿼리할 PQL 식입니다. |
| `predicateType` | 아래의 쿼리 식에 대한 설명 유형입니다 `predicateExpression`. 현재 이 속성에 대해 허용된 유일한 값은 입니다 `pql/text`. |
| `predicateModel` | 프로필 데이터를 기반으로 하는 [!DNL Experience Data Model] (XDM) 스키마의 이름입니다. |

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
| `state` | 미리 보기 작업의 현재 상태입니다. 처음 만들 때 &quot;NEW&quot; 상태가 됩니다. 그 후 처리가 완료될 때까지 &quot;RUNNING&quot; 상태가 되며, 여기서 &quot;RESULT_READY&quot; 또는 &quot;FAILED&quot;가 됩니다. |
| `previewId` | 다음 섹션에 설명된 대로 예측 또는 미리 보기를 볼 때 조회 목적으로 사용되는 미리 보기 작업의 ID입니다. |

## 특정 미리 보기 결과 검색 {#get-preview}

종단점에 GET 요청을 만들고 요청 경로에 미리 보기 ID를 제공하여 특정 미리 보기에 대한 자세한 정보를 검색할 수 `/preview` 있습니다.

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
| `results` | 관련 ID와 함께 엔티티 ID 목록입니다. 제공된 링크를 사용하여 [[!DNL 프로필 액세스 API]를 사용하여 지정된 엔터티를 조회할 수 있습니다](../../profile/api/entities.md). |

## 특정 예상 작업의 결과 검색 {#get-estimate}

미리 보기 작업을 만든 후에는 종단점에 대한 GET 요청 경로 `previewId` `/estimate` 에서 해당 작업을 사용하여 예상 대상 크기, 신뢰 구간 및 오류 표준 편차 등 세그먼트 정의에 대한 통계 정보를 볼 수 있습니다.

**API 형식**

```http
GET /estimate/{PREVIEW_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{PREVIEW_ID}` | 예상 작업은 미리 보기 작업을 만들 때만 트리거되며 두 작업은 조회 목적으로 동일한 ID 값을 공유합니다. 특히 미리 보기 작업을 만들 때 반환되는 `previewId` 값입니다. |

**요청**

다음 요청은 특정 예상 작업의 결과를 가져옵니다.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/estimate/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 예상 작업의 세부 사항과 함께 HTTP 상태 200을 반환합니다.

```json
{
    "estimatedSize": 0,
    "numRowsToRead": 1,
    "state": "RESULT_READY",
    "profilesReadSoFar": 1,
    "standardError": 0,
    "error": {
        "description": "",
        "traceback": ""
    },
    "profilesMatchedSoFar": 0,
    "totalRows": 1,
    "confidenceInterval": "95%",
    "_links": {
        "preview": "https://platform.adobe.io/data/core/ups/preview/app-32be0328-3f31-4b64-8d84-acd0c4fbdad3/execution/0?previewQueryId=e890068b-f5ca-4a8f-a6b5-af87ff0caac3"
    }
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `state` | 미리 보기 작업의 현재 상태입니다. 처리가 완료될 때까지 &quot;RUNNING&quot;이 되며 이 시점에서 &quot;RESULT_READY&quot; 또는 &quot;FAILED&quot;가 됩니다. |
| `_links.preview` | 미리 보기 작업의 현재 상태가 &quot;RESULT_READY&quot;인 경우 이 속성은 예상 값을 볼 수 있는 URL을 제공합니다. |

## 다음 단계

이 가이드를 읽고 나면 미리 보기 및 예상 작업 방법을 더 잘 이해할 수 있습니다. 다른 [!DNL Segmentation Service] API 끝점에 대한 자세한 내용은 [세그멘테이션 서비스 개발자 가이드 개요를 참조하십시오](./overview.md).