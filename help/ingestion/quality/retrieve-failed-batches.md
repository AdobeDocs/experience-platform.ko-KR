---
keywords: Experience Platform;홈;인기 항목;실패한 배치 검색;실패한 배치;배치 수집;배치 수집;실패한 배치;실패한 배치 가져오기;실패한 배치 가져오기;실패한 배치 가져오기;실패한 배치 다운로드;실패한 배치 다운로드;
solution: Experience Platform
title: 데이터 액세스 API를 사용하여 실패한 일괄 처리 검색
type: Tutorial
description: 이 자습서에서는 데이터 수집 API를 사용하여 실패한 배치에 대한 정보를 검색하는 단계를 다룹니다.
exl-id: 5fb9f28d-091e-4124-8d8e-b8a675938d3a
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 13%

---

# 데이터 액세스 API를 사용하여 실패한 일괄 처리 검색

Adobe Experience Platform은 데이터를 업로드하고 수집하는 두 가지 방법을 제공합니다. 다양한 파일 형식(예: CSV)을 사용하여 데이터를 삽입할 수 있는 일괄 처리 수집이나 스트리밍 끝점을 사용하여 실시간으로 해당 데이터를 [!DNL Platform]에 삽입할 수 있는 스트리밍 수집을 사용할 수 있습니다.

이 자습서에서는 [!DNL Data Ingestion] API를 사용하여 실패한 일괄 처리에 대한 정보를 검색하는 단계를 다룹니다.

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): [!DNL Experience Platform]에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
- [[!DNL Data Ingestion]](../home.md): 데이터를 [!DNL Experience Platform]에 보낼 수 있는 메서드입니다.

### 샘플 API 호출 읽기

이 튜토리얼에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서의 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request)에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

[!DNL Platform] API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 튜토리얼을 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출의 필수 헤더 각각에 대한 값이 제공됩니다.

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

[!DNL Schema Registry]에 속하는 리소스를 포함한 [!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 격리됩니다. [!DNL Platform] API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>[!DNL Platform]의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하십시오.

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

- `Content-Type: application/json`

### 샘플 일괄 처리 실패

이 자습서에서는 아래 표시된 대로 월 값을 **00**(으)로 설정하는 형식이 잘못된 샘플 데이터를 사용합니다.

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

잘못된 타임스탬프로 인해 위의 페이로드가 XDM 스키마에 대해 제대로 확인되지 않습니다.

## 실패한 일괄 처리 검색

**API 형식**

```http
GET /batches/{BATCH_ID}/failed
```

| 속성 | 설명 |
| -------- | ----------- |
| `{BATCH_ID}` | 조회 중인 배치 ID입니다. |

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

위의 응답을 사용하여 성공한 일괄 처리의 청크와 실패한 청크를 확인할 수 있습니다. 이 응답에서 `part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json` 파일에 실패한 일괄 처리가 포함되어 있음을 확인할 수 있습니다.

## 실패한 일괄 처리 다운로드

배치에서 실패한 파일을 알고 있으면 실패한 파일을 다운로드하여 오류 메시지를 확인할 수 있습니다.

**API 형식**

```http
GET /batches/{BATCH_ID}/failed?path={FAILED_FILE}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{BATCH_ID}` | 실패한 파일이 포함된 배치의 ID입니다. |
| `{FAILED_FILE}` | 서식이 실패한 파일의 이름입니다. |

**요청**

다음 요청을 사용하면 수집 오류가 발생한 파일을 다운로드할 수 있습니다.

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

이전에 수집된 배치에 잘못된 날짜-시간이 있으므로 다음 유효성 검사 오류가 표시됩니다.

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

이 자습서를 읽은 후 실패한 배치에서 오류를 검색하는 방법을 배웠습니다. 일괄 처리 수집에 대한 자세한 내용은 [일괄 처리 수집 개발자 안내서](../batch-ingestion/overview.md)를 참조하십시오. 스트리밍 수집에 대한 자세한 내용은 [스트리밍 연결 만들기 자습서](../tutorials/create-streaming-connection.md)를 참조하십시오.

## 부록

이 섹션에는 발생할 수 있는 다른 수집 오류 유형에 대한 정보가 포함되어 있습니다.

### 잘못된 형식의 XDM

이전 예제 흐름의 타임스탬프 오류와 마찬가지로 이러한 오류는 잘못된 형식의 XDM으로 인해 발생합니다. 이러한 오류 메시지는 문제의 특성에 따라 달라집니다. 따라서 구체적인 오류 예는 표시되지 않습니다.

### 누락되었거나 잘못된 조직 ID

이 오류는 조직 ID가 페이로드에서 누락된 경우 표시됩니다.

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

이 오류는 `xdmMeta`에 대한 `schemaRef`이(가) 누락된 경우 표시됩니다.

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

### 소스 이름 누락

헤더의 `source`에 `name`이(가) 없는 경우 이 오류가 표시됩니다.

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

### XDM 엔티티 누락

이 오류는 `xdmEntity`이(가) 없는 경우 표시됩니다.

```json
{
    "_validationErrors": [
        {
            "message": "Payload body is missing xdmEntity"
        }
    ]
}
```
