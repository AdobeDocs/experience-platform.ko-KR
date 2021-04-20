---
keywords: Experience Platform;home;popular topics;data prep;api guide;sample data
solution: Experience Platform
title: 샘플 데이터 API 끝점
topic: sample data
description: 'Adobe Experience Platform API의 ''/samples'' 끝점을 사용하여 매핑 샘플 데이터를 프로그래밍 방식으로 검색, 만들기, 업데이트 및 확인할 수 있습니다. '
translation-type: tm+mt
source-git-commit: a2c966ae2401faa572cbba974ce6f572d5280a8f
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 4%

---


# 샘플 데이터 끝점

매핑 세트에 대한 스키마를 만들 때 샘플 데이터를 사용할 수 있습니다. 데이터 준비 API의 `/samples` 끝점을 사용하여 프로그래밍 방식으로 샘플 데이터를 검색, 만들기 및 업데이트할 수 있습니다.

## 목록 샘플 데이터

`/samples` 종단점에 GET 요청을 하여 조직에 대한 모든 매핑 샘플 데이터 목록을 가져올 수 있습니다.

**API 형식**

`/samples` 끝점은 결과를 필터링하는 데 도움이 되는 여러 쿼리 매개 변수를 지원합니다. 현재 요청의 일부로 `start` 및 `limit` 매개 변수를 모두 포함해야 합니다.

```http
GET /samples?limit={LIMIT}&start={START}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{LIMIT}` | **필수 여부**. 반환된 매핑 샘플 데이터의 수를 지정합니다. |
| `{START}` | **필수 여부**. 결과 페이지의 오프셋을 지정합니다. 결과의 첫 페이지를 가져오려면 값을 `start=0`으로 설정합니다. |

**요청**

다음 요청은 IMS 조직 내에서 마지막 2개의 매핑 샘플 데이터를 검색합니다.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/samples?limit=2&start=0 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 샘플 데이터를 매핑하는 마지막 두 개체에 대한 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
    "data": [
        {
            "id": "2a429a0057ce47109a4b3e2bc256d755",
            "version": 0,
            "createdDate": 1582250863000,
            "modifiedDate": 1582250863000,
            "createdBy": "acp_xql_gateway",
            "modifiedBy": "acp_xql_gateway",
            "sampleData": "{\"id\":\"\",\"first_name\":\"\",\"last_name\":\"\",\"email\":\"\",\"gender\":\"\",\"ip_address\":\"\"}",
            "sampleType": "JSON"
        },
        {
            "id": "0248bfb352214f908bdd6cf9c19447e1",
            "version": 0,
            "createdDate": 1582250892000,
            "modifiedDate": 1582250892000,
            "createdBy": "acp_xql_gateway",
            "modifiedBy": "acp_xql_gateway",
            "sampleData": "{\"id\":\"\",\"first_name\":\"\",\"last_name\":\"\",\"email\":\"\",\"gender\":\"\",\"ip_address\":\"\"}",
            "sampleType": "JSON"
        }
    ],
    "_page": {
        "count": 2,
        "limit": 2
    }
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `sampleData` |  |
| `sampleType` |  |

## 샘플 데이터 만들기

`/samples` 끝점에 POST 요청을 하여 샘플 데이터를 만들 수 있습니다.

```http
POST /samples
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/samples \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Smith\", \"id\": \"3197210762560\"}",
    "sampleType": "JSON"    
  }'
```

**응답**

성공적인 응답은 새로 만든 샘플 데이터에 대한 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
    "id": "1fc0b6c20bae49d8ab33209ed126bdcd",
    "version": 0,
    "createdDate": 1615335404492,
    "modifiedDate": 1615335404492,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sampleData": "{\"FirstName\":\"carl\",\"LastName\":\"hooper\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```

## 파일을 업로드하여 샘플 데이터 만들기

`/samples/upload` 끝점에 POST 요청을 하여 파일을 사용하여 샘플 데이터를 만들 수 있습니다.

**API 형식**

```http
POST /samples/upload
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/samples \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: multipart/form-data' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -F 'file=@{PATH_TO_FILE}.json'
```

**응답**

성공적인 응답은 새로 만든 샘플 데이터에 대한 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
    "id": "1fb33209ed126bdcdc0b6c20bae49d8a",
    "version": 0,
    "createdDate": 1615335404492,
    "modifiedDate": 1615335404492,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sampleData": "{\"FirstName\":\"carl\",\"LastName\":\"hooper\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```

## 특정 샘플 데이터 개체 찾기

`/samples` 끝점에 GET 요청 경로에 해당 ID를 제공하여 샘플 데이터의 특정 개체를 찾을 수 있습니다.

**API 형식**

```http
GET /samples/{SAMPLE_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{SAMPLE_ID}` | 검색할 샘플 데이터 개체의 ID입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/samples/1fc0b6c20bae49d8ab33209ed126bdcd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 검색하려는 샘플 데이터 개체의 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
    "id": "1fc0b6c20bae49d8ab33209ed126bdcd",
    "version": 0,
    "createdDate": 1615335404000,
    "modifiedDate": 1615335404000,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sampleData": "{\"FirstName\":\"carl\",\"LastName\":\"hooper\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```

## 샘플 데이터 업데이트

PUT 요청 경로에서 `/samples` 끝점에 해당 ID를 제공하여 특정 샘플 데이터 개체를 업데이트할 수 있습니다.

**API 형식**

```http
PUT /samples/{SAMPLE_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{SAMPLE_ID}` | 업데이트할 샘플 데이터 개체의 ID. |

**요청**

다음 요청은 지정된 샘플 데이터를 업데이트합니다. 특히 성을 &quot;Smith&quot;에서 &quot;Lee&quot;로 업데이트합니다.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/conversion/samples/1fc0b6c20bae49d8ab33209ed126bdcd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Lee\", \"id\": \"3197210762560\"}",
    "sampleType": "JSON"    
  }'
```

**응답**

성공적인 응답은 업데이트된 샘플 데이터에 대한 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
    "id": "1fc0b6c20bae49d8ab33209ed126bdcd",
    "version": 1,
    "createdDate": 1615335404000,
    "modifiedDate": 1615337870375,
    "createdBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "modifiedBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Lee\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```
