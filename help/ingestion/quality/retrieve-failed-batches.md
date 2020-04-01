---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 실패한 배치 검색
topic: overview
translation-type: tm+mt
source-git-commit: 4817162fe2b7cbf4ae4c1ed325db2af31da5b5d3

---


# API를 사용하여 실패한 배치 검색

Adobe Experience Platform은 데이터를 업로드하고 인제스트하는 두 가지 방법을 제공합니다. CSV와 같은 다양한 파일 형식을 사용하여 데이터를 삽입할 수 있는 일괄 처리 방법을 사용하거나 스트리밍 끝점을 사용하여 실시간으로 플랫폼에 데이터를 삽입할 수 있는 스트리밍 통합 기능을 사용할 수 있습니다.

이 자습서에서는 데이터 통합 API를 사용하여 실패한 배치에 대한 정보를 검색하는 단계를 설명합니다.

## 시작하기

이 가이드는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

- [XDM(Experience Data Model) 시스템](../../xdm/home.md):Adobe Experience Platform을 통해 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
- [데이터 통합](../home.md):Experience Platform으로 데이터를 전송할 수 있는 메서드입니다.

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서에서 API 호출 [예를 읽는](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

플랫폼 API를 호출하려면 먼저 [인증 자습서를](../../tutorials/authentication.md)완료해야 합니다. 인증 튜토리얼을 완료하면 다음과 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값이 제공됩니다.

- 인증:베어러 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

스키마 레지스트리에 속하는 리소스를 비롯하여 경험 플랫폼의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. 플랫폼 API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 플랫폼의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서를](../../sandboxes/home.md)참조하십시오.

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형: `application/json`

### 샘플 실패한 일괄 처리

이 자습서는 아래 보기와 같이 달의 값을 00으로 설정하는 잘못된 형식의 타임스탬프가 있는 샘플 데이터를 **사용합니다**.

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

잘못된 형식의 타임스탬프로 인해 위의 페이로드가 XDM 스키마에 대해 올바르게 확인되지 않습니다.

## 실패한 배치 검색

**API 형식**

```http
GET /batches/{BATCH_ID}/failed
```

| 속성 | 설명 |
| -------- | ----------- |
| `{BATCH_ID}` | 조회하고 있는 배치의 ID입니다. |

**요청**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Cache-Control: no-cache" \
  -H "Content-Type: application/json" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}
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

위의 응답으로, 성공하고 실패한 일괄 처리를 볼 수 있습니다. 이 응답에서 파일에 실패한 일괄 처리가 `part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json` 포함되어 있음을 확인할 수 있습니다.

## 실패한 일괄 처리 다운로드

일괄 처리에서 실패한 파일을 알고 나면 실패한 파일을 다운로드하여 오류 메시지가 무엇인지 확인할 수 있습니다.

**API 형식**

```http
GET /batches/{BATCH_ID}/failed?path={FAILED_FILE}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{BATCH_ID}` | 실패한 파일을 포함하는 일괄 처리의 ID입니다. |
| `{FAILED_FILE}` | 형식이 실패한 파일의 이름입니다. |

**요청**

다음 요청을 통해 통합 오류가 있는 파일을 다운로드할 수 있습니다.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path={FAILED_FILE}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

이전에 인제스트한 일괄 처리에 잘못된 날짜 시간이 있으므로 다음 유효성 확인 오류가 표시됩니다.

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

이 자습서를 읽은 후 실패한 배치에서 오류를 검색하는 방법을 알아보았습니다. 일괄 처리에 대한 자세한 내용은 [일괄 처리 통합 개발자 안내서를](../batch-ingestion/overview.md)참조하십시오. 스트리밍 인제스트에 대한 자세한 내용은 스트리밍 연결 [만들기 자습서를](../tutorials/create-streaming-connection.md)참조하십시오.

## 부록

이 섹션에는 발생할 수 있는 다른 통합 오류 유형에 대한 정보가 포함되어 있습니다.

### 형식이 잘못된 XDM

이전 예제 흐름의 타임스탬프 오류와 마찬가지로 이러한 오류는 XDM 형식이 잘못되었기 때문입니다. 이러한 오류 메시지는 문제의 특성에 따라 달라집니다. 따라서 특정 오류 예는 표시되지 않습니다.

### IMS 조직 ID가 없거나 잘못되었습니다.

페이로드에서 IMS 조직 ID가 누락된 경우 이 오류가 표시됩니다.

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{IMS_ORG}@AdobeOrg] Message has an absent or wrong ims org in the header"
    }
}
```

### XDM 스키마 누락

이 오류는 `schemaRef` 에 대한 `xdmMeta` 내용이 누락된 경우에 표시됩니다.

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{IMS_ORG}@AdobeOrg] Message has unknown xdm format"
    }
}
```

### 소스 이름이 없습니다.

이 오류는 헤더에 `source` 해당 헤더가 누락된 경우 표시됩니다 `name`.

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

### XDM 엔터티 누락

이 오류는 `xdmEntity` 존재하지 않는 경우에 표시됩니다.

```json
{
    "_validationErrors": [
        {
            "message": "Payload body is missing xdmEntity"
        }
    ]
}
```
