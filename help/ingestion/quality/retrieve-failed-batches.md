---
keywords: Experience Platform;홈;인기 항목;실패한 배치 검색;실패한 배치;배치 수집;배치 처리 실패;배치 가져오기;실패한 배치 가져오기;실패한 배치 다운로드;실패한 배치 다운로드;실패한 배치 다운로드
solution: Experience Platform
title: 데이터 액세스 API를 사용하여 실패한 배치 검색
type: Tutorial
description: 이 자습서에서는 데이터 수집 API를 사용하여 실패한 배치에 대한 정보를 검색하는 단계를 설명합니다.
exl-id: 5fb9f28d-091e-4124-8d8e-b8a675938d3a
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 2%

---

# 데이터 액세스 API를 사용하여 실패한 배치 검색

Adobe Experience Platform에서는 데이터를 업로드하고 수집하는 두 가지 방법을 제공합니다. 일괄 처리 수집을 사용할 수 있습니다. 이 방법을 통해 다양한 파일 유형(예: CSV)을 사용하여 해당 데이터를 삽입하거나 스트리밍 수집 기능을 사용하여에 데이터를 삽입할 수 있습니다 [!DNL Platform] 스트리밍 끝점을 실시간으로 사용합니다.

이 자습서에서는 을 사용하여 실패한 배치에 대한 정보를 검색하는 단계를 설명합니다 [!DNL Data Ingestion] API.

## 시작하기

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다.
- [[!DNL Data Ingestion]](../home.md): 데이터를 보낼 수 있는 메서드입니다 [!DNL Experience Platform].

### 샘플 API 호출 읽기

이 자습서에서는 요청 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 에서 [!DNL Experience Platform] 문제 해결 가이드.

### 필수 헤더에 대한 값을 수집합니다

을 호출하려면 [!DNL Platform] API를 먼저 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 모든 히트에 필요한 각 헤더에 대한 값이 제공됩니다 [!DNL Experience Platform] 아래에 표시된 대로 API 호출:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

의 모든 리소스 [!DNL Experience Platform]에 속했던 것 포함 [!DNL Schema Registry]은 특정 가상 샌드박스로 구분됩니다. 에 대한 모든 요청 [!DNL Platform] API에는 작업이 발생할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>샌드박스에 대한 자세한 내용은 [!DNL Platform]를 참조하고 [샌드박스 개요 설명서](../../sandboxes/home.md).

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 헤더가 필요합니다.

- `Content-Type: application/json`

### 샘플 실패 일괄 처리

이 자습서에서는 월 값을 설정하는 잘못된 형식의 타임스탬프가 있는 샘플 데이터를 사용합니다 **00**&#x200B;아래에 표시된 것처럼:

```json
{
    "body": {
        "xdmEntity": {
            "id": "c8d11988-6b56-4571-a123-b6ce74236036",
            "timestamp": "2018-00-10T22:07:56Z",
            "environment": {
                "browserDetails": {
                    "userAgent": "Mozilla\/5.0 (Windows NT 5.1) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/29.0.1547.57 Safari\/537.36 OPR\/16.0.1196.62",
                    "acceptLanguage": "en-US",
                    "cookiesEnabled": true,
                    "javaScriptVersion": "1.6",
                    "javaEnabled": true
                },
                "colorDepth": 32,
                "viewportHeight": 799,
                "viewportWidth": 414
            }
        }
    }
}
```

잘못된 형식의 타임스탬프로 인해 위의 페이로드가 XDM 스키마에 대해 제대로 유효성 검사가 수행되지 않습니다.

## 실패한 배치 검색

**API 형식**

```http
GET /batches/{BATCH_ID}/failed
```

| 속성 | 설명 |
| -------- | ----------- |
| `{BATCH_ID}` | 조회 중인 배치의 ID입니다. |

**요청**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

```json
{
    "data": [
        {
            "name": "_SUCCESS",
            "length": "0",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/{BATCH_ID}/failed?path=_SUCCESS"
                }
            }
        },
        {
            "name": "part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json",
            "length": "1800",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/{BATCH_ID}/failed?path=part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 2
    }
}
```

위의 응답으로, 성공적으로 및 실패한 배치 청크를 확인할 수 있습니다. 이 응답에서 파일이 `part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json` 실패한 배치를 포함합니다.

## 실패한 배치 다운로드

일괄 처리에서 실패한 파일을 알고 있으면 실패한 파일을 다운로드하여 오류 메시지가 무엇인지 확인할 수 있습니다.

**API 형식**

```http
GET /batches/{BATCH_ID}/failed?path={FAILED_FILE}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{BATCH_ID}` | 실패한 파일이 포함된 일괄 처리의 ID입니다. |
| `{FAILED_FILE}` | 형식이 실패한 파일의 이름입니다. |

**요청**

다음 요청을 통해 수집 오류가 있는 파일을 다운로드할 수 있습니다.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path={FAILED_FILE}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

이전에 수집된 일괄 처리에 잘못된 날짜 시간이 있으므로 다음 유효성 검사 오류가 표시됩니다.

```json
{
    "_validationErrors": [
        {
            "causingExceptions": [],
            "keyword": "format",
            "message": "[2018-00-23T22:07:01Z] is not a valid date-time. Expected [yyyy-MM-dd'T'HH:mm:ssZ, yyyy-MM-dd'T'HH:mm:ss.[0-9]{1-9}Z, yyyy-MM-dd'T'HH:mm:ss[+-]HH:mm, yyyy-MM-dd'T'HH:mm:ss.[0-9]{1,9}[+-]HH:mm]",
            "pointerToViolation": "#/timestamp",
            "schemaLocation": "#/properties/timestamp"
        }
    ]
}
```

## 다음 단계

이 자습서를 읽은 후 실패한 배치에서 오류를 검색하는 방법을 알아보았습니다. 일괄 처리에 대한 자세한 내용은 [배치 수집 개발자 안내서](../batch-ingestion/overview.md). 스트리밍 수집에 대한 자세한 내용은 [스트리밍 연결 만들기 자습서](../tutorials/create-streaming-connection.md).

## 부록

이 섹션에는 발생할 수 있는 다른 수집 오류 유형에 대한 정보가 들어 있습니다.

### 잘못된 형식의 XDM

이전 예제 흐름의 타임스탬프 오류와 마찬가지로 이러한 오류는 잘못된 형식의 XDM 때문입니다. 이러한 오류 메시지는 문제의 특성에 따라 달라집니다. 따라서 특정 오류 예는 표시되지 않습니다.

### 조직 ID가 없거나 잘못되었습니다.

페이로드에서 조직 ID가 누락되었거나 잘못된 경우 이 오류가 표시됩니다.

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{ORG_ID}@AdobeOrg] Message has an absent or wrong ims org in the header"
    }
}
```

### XDM 스키마 누락

이 오류는 `schemaRef` 대상 `xdmMeta` 이(가) 없습니다.

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{ORG_ID}@AdobeOrg] Message has unknown xdm format"
    }
}
```

### 소스 이름이 없습니다.

이 오류는 `source` 헤더에서 헤더에 `name`.

```json
{
    "_errors":{
        "_streamingValidation": [
            {
                "message": "Payload header is missing Source Name"
            }
        ]
    }
}
```

### XDM 엔터티가 없습니다.

이 오류는 가 없는 경우 표시됩니다 `xdmEntity` 표시합니다.

```json
{
    "_validationErrors": [
        {
            "message": "Payload body is missing xdmEntity"
        }
    ]
}
```
